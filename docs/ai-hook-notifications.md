# AHAwork 通知系統 — AI Hook 串接指南

> 讓 AI 工具（Claude Code、Cursor、Windsurf 等）在任務完成時自動發送通知到 AHAwork。

---

## 原理

AHAwork 註冊了 `cowork://` Deep Link。任何程式只要執行一行 `open` 指令，就能觸發：

1. **macOS 原生通知**（App 在背景或不同專案時彈出系統橫幅）
2. **應用內 Toast**（App 在前景且同一專案時顯示）
3. **通知中心**（鈴鐺 Badge + 通知面板，不管哪種方式都會收錄，可點擊跳轉）

### 通知提醒方式（互斥）

| 場景 | 提醒方式 |
|------|---------|
| App 背景 | macOS 系統通知 |
| App 前景 + 不同專案 | macOS 系統通知 |
| App 前景 + 同專案 | in-app Toast |

不管哪種提醒方式，通知中心（鈴鐺）都會收錄。

---

## 指令格式

```bash
open "cowork://notify?terminal=終端機名稱&type=complete&message=通知內容&project=專案路徑&session_id=終端機ID"
```

| 參數 | 必填 | 說明 | 預設值 |
| --- | --- | --- | --- |
| `terminal` | **是** | 終端機的顯示名稱（fallback 用，App 內有自訂名稱時會優先顯示自訂名稱） | — |
| `type` | 否 | `complete`（任務完成 ✅）或 `action`（需要處理 ⚠️） | `complete` |
| `message` | 否 | 通知訊息內容 | `任務完成` |
| `project` | 否 | 專案資料夾的絕對路徑（用於跨專案跳轉 + 通知標題顯示「專案 > 分頁」） | 空值 |
| `session_id` | 否 | 終端機 session ID（由 `COWORK_SESSION_ID` env 自動提供，用於精確匹配） | 空值 |

### 通知標題顯示邏輯

通知標題格式為 **「專案名 > 分頁名」**，例如 `Cowork-stable > 我的 Claude`。

分頁名解析優先序：
1. App 內自訂的 tab 名稱（用戶重命名過的，`isCustomLabel`）
2. Deep Link 的 `terminal` 參數（如 "Claude Code"）
3. 動態 terminal title（shell/CLI 設定的）

### 快速範例

```bash
# 最簡單 — 只需終端機名稱
open "cowork://notify?terminal=Claude"

# 帶訊息
open "cowork://notify?terminal=Claude&message=單元測試全部通過"

# 需要處理（顯示 ⚠️ 而非 ✅）
open "cowork://notify?terminal=Build&type=action&message=編譯失敗，請查看錯誤"

# 指定專案路徑（跨專案跳轉 + 標題顯示專案名）
open "cowork://notify?terminal=Deploy&message=部署完成&project=/Users/me/projects/my-app"

# 帶 session ID（精確匹配終端機）
open "cowork://notify?terminal=Claude&session_id=abc123&project=/Users/me/projects/my-app"
```

---

## Claude Code Hook 設定

### 自動串接（推薦）

在 AHAwork 的終端機中啟動 Claude Code 時，App 會自動注入 `COWORK_SESSION_ID` 環境變數。Hook 腳本會自動讀取這個 ID，實現精確的終端機匹配和跳轉。

在專案的 `.claude/settings.json` 中設定：

```jsonc
{
  "hooks": {
    "Stop": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "cat | \"$CLAUDE_PROJECT_DIR\"/.claude/hooks/notify-macos.sh"
          }
        ]
      }
    ]
  }
}
```

### Hook 腳本行為

`notify-macos.sh` 會：
1. 從 Claude Code 回覆中提取最後 2 行作為通知內容
2. 跳過純確認訊息（如 "任務完成"），避免重複通知
3. 透過 `cowork://` Deep Link 發送通知
4. 自動帶入 `COWORK_SESSION_ID`（精確匹配）和 `CLAUDE_PROJECT_DIR`（跨專案跳轉）
5. 如果 Deep Link 失敗（dev 環境），fallback 到 `osascript` 原生通知

### 終端機命名

在 AHAwork 中雙擊終端機 tab 可重命名。重命名後的名稱會自動顯示在通知標題中（優先於 Deep Link 的 `terminal` 參數）。

啟動 Claude Code 前也可設定 `COWORK_TERMINAL` 環境變數：

```bash
export COWORK_TERMINAL="我的 Claude" && claude
```

不設定則預設使用 "Claude Code"。

---

## Cursor / Windsurf 等其他 AI 工具

這些工具目前沒有內建 hook 系統，但可以透過以下方式串接：

### 方法 1：在 AI 對話中請求

直接在提示中告訴 AI：

```
完成後請執行：open "cowork://notify?terminal=Cursor&message=任務完成"
```

### 方法 2：Shell Script 包裝

建立一個 `notify.sh`，在任何終端機中使用：

```bash
#!/bin/bash
# ~/bin/notify.sh — 發送 AHAwork 通知
TERMINAL="${1:-Terminal}"
MESSAGE="${2:-任務完成}"
TYPE="${3:-complete}"
open "cowork://notify?terminal=${TERMINAL}&type=${TYPE}&message=${MESSAGE// /+}"
```

使用方式：

```bash
chmod +x ~/bin/notify.sh

# 基本使用
~/bin/notify.sh "Cursor" "程式碼審查完成"

# 需要處理
~/bin/notify.sh "Build" "編譯失敗" "action"
```

### 方法 3：搭配任何長時間命令

```bash
# 測試跑完後通知
pnpm test && open "cowork://notify?terminal=Test&message=測試全部通過" || open "cowork://notify?terminal=Test&type=action&message=測試失敗"

# build 完成後通知
cargo build --release; open "cowork://notify?terminal=Build&message=Build+完成"
```

---

## 通知行為說明

| 行為 | 說明 |
| --- | --- |
| App 在前景 + 同專案 | in-app Toast 提示 |
| App 在前景 + 不同專案 | macOS 系統通知橫幅 |
| App 在背景 | macOS 系統通知橫幅 |
| 點擊鈴鐺 | 展開通知面板，顯示所有通知（最新在上） |
| 點擊通知項目 | 自動切換專案 + 跳轉到對應終端機 tab（含 editor area） |
| `project` 為空 | 自動搜尋所有已開啟專案 |
| `session_id` 提供時 | 精確匹配終端機（支援 reconnect 後的 ID 變化） |
| 通知上限 | 最多 50 則，超出時自動清除最舊的已讀通知 |
| 通知標題格式 | 「專案名 > 分頁名」（如 `Cowork-stable > 我的 Claude`） |

---

## 疑難排查

```bash
# 測試通知是否正常
open "cowork://notify?terminal=Test&message=Hello&project=$(pwd)"

# 查看 AHAwork 日誌（Rust 端）
tail -f ~/Library/Logs/com.cowork.app/AHAwork.log | grep notification

# 查看前端日誌（需在 App 內按 Cmd+Option+I 開啟 DevTools）
# Console 搜尋 "[notification]" 可看到完整的標題解析和跳轉流程
```

如果通知沒有出現：

1. 確認 AHAwork 正在執行
2. 確認 macOS「系統設定 → 通知」中 AHAwork 已允許通知
3. 檢查日誌中是否有 `[notification]` 開頭的錯誤訊息
4. 確認 Deep Link URL 格式正確（特殊字元需 URL encode）

### 開發環境限制

`cowork://` URL scheme 需要打包成 `.app` 後由 macOS 註冊。`cargo tauri dev` **不會註冊 URL scheme**。

開發環境的替代方案：

- Claude Code hook 已內建 `osascript` fallback — dev 環境自動改用 macOS 原生通知
- 手動測試 Deep Link 需先 `cargo tauri build --debug`，然後執行產出的 `.app`
