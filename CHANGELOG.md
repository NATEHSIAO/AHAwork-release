# AHAwork Changelog / 版本更新記錄

---

## v0.1.35 — 2026-05-01

### 新功能
- 表格內支援行內勾選框 — 可在表格儲存格內插入可點擊的 checkbox

### 問題修復
- 修復終端機長時間使用後出現文字亂碼的問題
- 修復終端機關閉需要按兩次的問題
- 修復底部終端機面板第一次點擊無法打開的問題
- 修復開啟專案時底部終端機面板不再預設開啟的問題
- 修復編輯器中圖片無法正常顯示的問題
- 修復圖片拖曳到終端機時路徑插入錯誤的問題
- 修復表格內勾選框存檔後消失的問題

### 體驗優化
- 終端機渲染引擎自動維護機制 — 大幅降低長時間使用後出現亂碼的機率
- 終端機關閉操作不再有延遲
- 底部終端機控制列重新設計 — 終端機名稱與關閉按鈕分組顯示，層次更清晰
- 拖曳圖片到終端機需按住 Shift，附浮動提示，避免誤操作
- 終端機 resize 後自動捲到底部

---

## v0.1.34 — 2026-04-25

### 問題修復
- 徹底修復切換專案或分頁後，終端機畫面出現亂碼的問題
- 修復背景閒置的終端機佔用過多記憶體的問題

### 體驗優化
- 終端機切換回來時不再閃爍或短暫空白

---

## v0.1.33 — 2026-04-25

### 新功能
- 自動更新：啟動時自動檢查新版本，可選擇立即更新、稍後提醒或跳過
- 版本資訊：在 Help 選單查看當前版本與歷史更新記錄
- 問題回報：Help 選單一鍵回報問題，自動附上系統資訊方便排查
- 更新說明：版本更新後自動顯示本次更新了什麼

### 問題修復
- 修復終端機在背景放久後畫面渲染異常的問題
- 修復終端機偶爾出現部分文字缺失的問題

---

## v0.1.32 — 2026-04-24

### 問題修復

**終端機**
- 修復切換專案或分頁後，終端機畫面出現亂碼的問題
- 修復切換回終端機時畫面會從頂部重新捲動的問題
- 修復第一個終端機分頁無法雙擊改名的問題
- 修復關閉 App 重新開啟後，所有終端機消失的問題
- 底部面板的「關閉」和「收起」按鈕分開，避免誤觸

**輸入**
- 修復中文輸入法選字後出現錯誤字元的問題
- 修復在終端機中無法貼上圖片的問題
- 修復 Shift+Enter 會貼上圖片而非換行的問題
- 修復提示框偶爾卡在畫面上不消失的問題

**檔案管理**
- 修復在深層資料夾新增檔案時輸入框不出現的問題
- 新增檔案時預設位置改為目前所在的資料夾
- 拖曳檔案到終端機現在需要按住 Shift 才會貼上路徑

---

## v0.1.31 — 2026-04-10

### 新功能
- 終端機任務完成時會收到桌面通知，點擊可直接跳到對應終端機
- 介面新增英文語系，可在設定中切換
- 分頁切換或專案切換後自動聚焦到內容區
- 新增檔案時直接建立在目前選取的資料夾內
- Git 暫存區支援整個資料夾一次加入
- 拖曳檔案到檔案櫃空白區域可移動到根目錄

### 問題修復
- 修復檔案拖曳成功卻顯示「移動失敗」的問題
- 修復 Git 暫存區的樹狀結構偶爾消失的問題
- 修復終端機最後一個分頁關閉後面板未自動收起的問題
- 修復通知功能在特定情境下閃退的問題

### What's New

**New Features**
- Native macOS notifications with foreground banner display
- Full i18n support (Traditional Chinese / English)
- Auto-focus content area on tab/project switch
- One-click terminal close with process group cleanup (MCP zombie fix)
- Create files in selected folder context
- Git folder staging, tag-hidden graph view
- Drag files to empty area to move to root directory

**Bug Fixes**
- Fix duplicate "move failed" toast on successful file drag
- Fix staged changes losing tree structure
- Fix bottom panel not collapsing after last terminal session close
- Fix UNUserNotificationCenter crash in dev mode

---

## v0.1.22 — 2026-03-30

### 更新內容

**問題修復**
- 修復切換專案時終端機黑屏問題（Session 恢復時序修正）
- 修復隱藏終端機持續 resize 導致行寬錯位（最小尺寸保護）
- 修復多終端機高負載下字形亂碼（WebGL 渲染穩定性優化，context 上限管控）

**新功能**
- 歡迎頁面支援拖拉資料夾開啟專案
- 終端機面板預設開啟

### What's New

**Bug Fixes**
- Fix terminal black screen when switching projects (session restore timing)
- Fix hidden terminal resize spam causing layout corruption (minimum size guard)
- Fix garbled text under heavy multi-terminal load (WebGL stability, context limit)

**New Features**
- Drag-and-drop folder to open project from welcome screen
- Terminal panel open by default

---

## v0.1.21 — 2026-03-30

### 更新內容

**新功能**
- 終端機自訂名稱：雙擊終端機 tab 可直接重新命名，支援底部面板、tab bar 及編輯區
- 自訂名稱保護：自訂名稱後，前景程序（如 Claude Code）的標題變更不會覆蓋自訂名稱

**問題修復**
- 修復 detached terminal（拉到編輯區）改名無效的問題

**其他**
- 更新發布腳本

### What's New

**New Features**
- Custom terminal tab names: double-click any terminal tab to rename it (bottom panel, tab bar, editor area)
- Auto-title protection: custom names persist even when foreground processes change the terminal title

**Bug Fixes**
- Fixed rename not working for terminals dragged to the editor area

**Other**
- Updated release scripts

---
## v0.1.18 — 2026-03-27

### 更新內容

**問題修復**
- 修復 Git Push 按鈕在多 Worktree 環境下不顯示的問題
- 修復終端機 Mutex 死鎖風險（lock ordering 統一）
- 修復 Git Graph 在多 Worktree 間互相覆蓋的問題
- 修復檔案櫃顯示模式（簡潔/完整）切換後未持久化的問題
- 修復多檔案拖放到終端機只寫入單一路徑的問題

**新功能**
- 編輯器 URL 自動偵測並轉為可點擊超連結
- 終端機內連結可點擊（外部 URL 開瀏覽器，檔案路徑在 App 內開啟）
- Tab 拖放到終端機自動寫入檔案路徑
- 外部檔案拖放到檔案櫃自動複製
- Tab 切換時檔案櫃自動定位並展開對應檔案
- 專案開啟後自動清理孤立 asset 圖片

**體驗優化**
- Git 統一 Refresh 機制（Promise.all 並行刷新）
- 消除 Git 雙重 Polling，降低 CPU 使用
- 檔案櫃顯示模式切換 Race Condition 防護

### What's New

**Bug Fixes**
- Fixed Git Push button not appearing in multi-worktree setups
- Fixed terminal Mutex deadlock risk (unified lock ordering)
- Fixed Git Graph data bleeding across worktrees
- Fixed file tree display mode not persisting across sessions
- Fixed multi-file drag to terminal only writing single path

**New Features**
- Auto-detect and linkify URLs in the editor
- Clickable links in terminal (URLs open browser, file paths open in app)
- Drag tabs to terminal to write file paths
- Drag external files to file tree to copy them into project
- Auto-expand and scroll to active file in file tree on tab switch
- Auto-cleanup orphaned asset images on project open

**Improvements**
- Unified Git refresh mechanism with parallel execution
- Eliminated dual Git polling to reduce CPU usage
- Race condition protection for file tree mode switching

---

## v0.1.17 — 2026-03-25

### 更新內容
- **檔案櫃顯示模式切換**：新增「簡潔模式」與「完整模式」切換，完整模式可顯示所有隱藏資料夾（dotfiles、node_modules 等）
- **重整檔案櫃按鈕恢復**：工具列新增重整按鈕，可快速刷新檔案樹
- **快捷鍵架構修復（第二輪）**：修復 outline toggle、nav 快捷鍵被系統攔截等問題，補強 Dispatcher 整合測試
- **終端機優化**：終端機相關補充修正

### What's New
- **File tree display mode**: Switch between "Simple" (hide dotfiles) and "Full" (show all files/folders)
- **Refresh button restored**: Quick refresh button added back to file tree toolbar
- **Keyboard shortcut fixes (round 2)**: Fixed outline toggle, nav shortcuts intercepted by WKWebView, added dispatcher integration tests
- **Terminal improvements**: Minor terminal fixes

---

## v0.1.16 — 2026-03-24

### 更新內容
- **快捷鍵架構重構**：統一 Dispatcher + Scope 機制，取代分散的事件監聯
- **終端機補充修正**：終端機相關 bug 修復

### What's New
- **Keyboard shortcut architecture overhaul**: Unified dispatcher + scope-based routing
- **Terminal fixes**: Minor terminal bug fixes

---

## v0.1.15 — 2026-03-24

### 更新內容
- 初始 Preview 發布版本

### What's New
- Initial Preview release
