# Security / 安全性

## Architecture / 架構

AHAwork is built on Tauri v2, which provides a security-first architecture:

AHAwork 基於 Tauri v2 打造，提供安全優先的架構：

- **Rust backend / Rust 後端** — All filesystem and process operations run in Rust, benefiting from Rust's memory safety guarantees (no buffer overflows, no use-after-free, no data races) / 所有檔案系統與程序操作都在 Rust 中執行，受益於 Rust 的記憶體安全保證（無緩衝區溢位、無釋放後使用、無資料競爭）
- **No Node.js runtime / 無 Node.js 運行時** — Unlike Electron apps, there is no Node.js process running alongside the app, eliminating an entire class of supply chain and runtime vulnerabilities / 與 Electron 不同，沒有 Node.js 程序伴隨運行，消除一整類供應鏈與運行時漏洞
- **IPC boundary / IPC 邊界** — The frontend (WebView) cannot directly access the filesystem or spawn processes. All operations go through explicitly defined Tauri Commands with type-checked parameters / 前端（WebView）無法直接存取檔案系統或產生程序。所有操作都透過明確定義的 Tauri Commands 與型別檢查的參數
- **CSP enforced / CSP 強制執行** — Content Security Policy is configured to restrict what the WebView can load and execute / 內容安全策略限制 WebView 可載入與執行的內容

## Local-first / 本地優先

AHAwork is designed to be local-first:

AHAwork 採用本地優先設計：

- Your files stay on your machine / 你的檔案留在你的電腦上
- No telemetry or analytics / 無遙測或分析

## Reporting / 回報問題

If you find a security issue, please open an issue or contact the maintainer directly.

如果你發現安全問題，請開 issue 或直接聯繫維護者。
