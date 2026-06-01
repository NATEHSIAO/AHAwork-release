# AHAwork Changelog / 版本更新記錄

---

## v0.1.39 — 2026-06-01

### 新功能
- **全文件展開模式** — 分頁群組右上角新增展開按鈕，一鍵把目前的文件或終端機放大到佔滿整個工作區（保留左側檔案櫃），專注閱讀或編輯；再按一下即可收回。支援所有文件類型，包含終端機。

### 問題修復
- 修復長時間使用後終端機區域整個變黑（黑屏）的問題 — 現在會自動偵測畫面失效並重建，不需重開 App
- 修復終端機長時間無回應時，背景或待機狀態下誤跳「終端機無回應」通知的問題
- 修復圖片拖曳到終端機（給 Claude Code）有時被擋住、無法插入檔案路徑的問題
- 修復在編輯器貼上 / 拖曳圖片時，偶爾被存到錯誤專案資料夾的問題 — 圖片現在只會存到目前開啟的專案
- 修復中文打到一半、切去終端機拉檔案後再繼續輸入，文字會變成散開注音的問題
- 修復把群組裡最後一個終端機分頁拖到其他群組時，終端機被意外關閉的問題

### 體驗優化
- Markdown 編輯器貼上 Markdown 文字時自動辨識並轉成排版後的樣子，不再原樣貼成純文字
- 沒有副檔名或特殊檔名的檔案（如 `.env.local`、`Dockerfile`、`Makefile`）現在可以直接開啟編輯
- 開啟大量終端機分頁時的資源管理優化 — 背景分頁自動休眠、切回時自動喚醒，長時間使用更穩定
- 終端機長時間無回應時，提供系統通知與一鍵恢復

### What's New
- **Full-screen expand mode** — a new expand button on each tab group blows the current document or terminal up to fill the whole workspace (file tree stays); click again to collapse. Works for every file type, including terminals.
- Fixed the terminal area going fully black after long sessions — failed canvases are now detected and rebuilt automatically, no restart needed
- Fixed false "terminal not responding" notifications while the app was in the background or idle
- Fixed images dropped onto the terminal (for Claude Code) sometimes being blocked instead of inserting the file path
- Fixed pasted/dropped images occasionally landing in the wrong project folder — images now always save to the currently open project
- Fixed Chinese IME input breaking into loose phonetic symbols after dragging a file into the terminal mid-composition
- Fixed the last terminal tab in a group being accidentally closed when dragged to another group
- Pasted Markdown is now auto-detected and rendered instead of staying as plain text
- Files with no or unusual extensions (`.env.local`, `Dockerfile`, `Makefile`…) are now editable
- Smarter resource handling with many terminal tabs — background tabs sleep and wake automatically

### Technical Notes (內部追蹤)
- 涵蓋內部版本：v0.1.9.2 ~ v0.1.9.4
- v0.1.9.2：Asset 儲存與 Workspace 註冊重構（workspace_registry 白名單 + drop/paste guard，杜絕跨專案污染）
- v0.1.9.3：Prod 終端機區 hotfix（LRU canvas 待機 + Canvas watchdog + Rust heartbeat + Channel cleanup 公開 API + pool 累積根因修 + deep-link reload-webview）
- v0.1.9.4：6 bug 修復（heartbeat is_visible / image→terminal DropRouter 短路 / Tiptap transformPastedText / DocumentFactory 預設 MonacoAdapter / IME blur+rAF focus 重建 / disposeGroup 跨 group stillReferenced 防護）+ 全文件展開模式（store-driven expandedSourceGroupId）
- Rust 126/126；TS 0 新 regression

---

## v0.1.37 — 2026-05-11

### 問題修復
- 修復「拖檔案到終端機沒按 Shift 卻被貼路徑」的問題 — 現在從 Finder、側邊欄、編輯器分頁三種來源拖曳行為都一致，沒按 Shift 不會誤貼路徑到 Claude Code 對話框
- 優化終端機渲染邏輯，徹底解決 Claude Code 等 TUI 程式畫面亂碼破版問題

### 新功能（小）
- 終端機新增「重新渲染」按鈕（工具列），快捷鍵 `Cmd+Alt+R` — TUI 程式畫面壞掉時不需殺進程，按一下強制重畫

### 體驗優化
- 分頁群組首項是終端機時，自動隱藏無意義的「上一頁/下一頁」按鈕

### What's New
- Fixed "files dropped on terminal getting pasted as paths without Shift" — now consistent across Finder, sidebar, and tab drags
- Optimized terminal rendering — fully resolves garbled output / layout breakage in TUI apps like Claude Code
- Terminal "Redraw" button (toolbar) and `Cmd+Alt+R` shortcut to force a redraw without killing the process
- Auto-hide prev/next nav icons when the first item in a tab group is a terminal

### Technical Notes (內部追蹤)
- 內部版本號：v0.1.9.1.f
- 拖曳系統重構：DropRouter 集中入口 + GlobalModifierState 統一 Shift 來源 + Fail-safe 預設
- ESLint `no-restricted-imports` rule 強制保護未來不再回歸
- 68 個新增測試（單元 44 + ATDD 24）/ typecheck 0 errors / 0 新 regression

---

## v0.1.36 — 2026-05-08

### 新功能
- DOCX / PPTX 文件預覽 — 在 app 內直接預覽 Word 和 PowerPoint 文件
  - DOCX: 標題顏色、項目符號、表格、底色框正確顯示
  - PPTX: 應用內全螢幕、滾輪/觸控板縮放、即時更新追蹤頁碼
- Markdown 編輯器區塊巢狀結構與拖曳排序 — 支援多層巢狀清單與跨層級區塊拖曳

### What's New
- Preview DOCX and PPTX files directly in AHAwork (headings, bullets, tables, shaded blocks; PPTX in-app fullscreen, scroll-to-zoom, live page tracking)
- Nested blocks and drag-and-drop reordering in the Markdown editor

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
