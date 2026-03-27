# AHAwork Changelog / 版本更新記錄

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
