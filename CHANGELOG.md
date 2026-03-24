# AHAwork Changelog / 版本更新記錄

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
