# edEdit

> 跨 macOS 與 iOS 的原生文字編輯器，整合筆記、Markdown 與原始碼編輯。

A native text editor for Mac and iPhone/iPad that brings notes, Markdown, and source code editing into one app.

---

## 為什麼選 edEdit · Why edEdit

- **真正原生** — macOS 用 AppKit、iOS 用 SwiftUI，沒有 web view 拖累體驗
- **跨平台一致** — 你的筆記與檔案在 Mac、iPhone、iPad 之間透過 iCloud 自動同步
- **不綁專屬格式** — 所有檔案就是 `.md` / `.txt` / `.swift` / `.json` 等標準文字格式，可隨時用其他 app 開啟
- **無廣告無追蹤** — 一次買斷 Pro，永久解鎖

---

## 主要功能 · Features

### 📝 筆記（Notes）
階層式標籤組織想法（如 `work/meeting/2026Q1`），透過 iCloud 跨裝置同步。從 iOS 內建備忘錄分享過來，自動轉換成 Markdown 並保留粗體、斜體、標題、清單、待辦。

### 📂 檔案（Files）
從「檔案」app、iCloud Drive、On My iPhone、第三方 provider 開啟並編輯任何文字檔。內建：
- 自動編碼偵測（UTF-8 / Big5 / Shift-JIS / GB18030 等）
- 多語言語法高亮（Swift、JavaScript、TypeScript、Python、Go、Rust、C/C++、Java、HTML、JSON、YAML、Shell、Markdown 等 17 種）
- 行號 gutter、深色／淺色主題
- 編輯後可直接存回原始位置

### ✏️ Markdown 專屬編輯體驗
- 鍵盤上方工具列：標題、粗體、斜體、清單、待辦、引用、連結、圖片
- 硬體鍵盤快速鍵：⌘B / ⌘I / ⌘K / ⌘E / ⌘1-6
- 智慧清單續行：清單行末按 Enter 自動續一個項目；空項目跳出清單
- 剪貼簿圖片直接貼進 Markdown，自動寫成圖檔放旁邊

### 📑 檔案比較（Pro）
直接在裝置上比對兩個檔案的差異，視覺化呈現增 / 刪 / 修改的行。

### 🔍 跨檔搜尋（Pro）
在你選定的資料夾內遞迴搜尋關鍵字，支援檔名 glob 過濾。

### 🤝 整合
- 從 Files app「Open in...」可直接打開到 edEdit
- Share Extension：從 Notes / Safari / Mail 任意 share sheet 進入
- 分享 / AirPrint / Find in Files 全部內建

---

## 系統需求 · Requirements

- iOS 16.0+
- macOS 12.0+

---

## 下載 · Download

App Store 連結待補。<!-- TODO: 上架後填上 -->

---

## 文件 · Documentation

- [快速開始 / Getting Started](docs/getting-started.md)
- [Markdown 編輯快速鍵 / Markdown Shortcuts](docs/markdown-shortcuts.md)
- [iCloud 同步設定 / iCloud Sync](docs/icloud-sync.md)
- [從備忘錄分享 / Sharing from Notes](docs/share-extension.md)
- [常見問題 / FAQ](docs/faq.md)

---

## 多語系支援 · Languages

繁體中文 · English · 日本語 · 简体中文

---

## 隱私 · Privacy

[隱私權政策 / Privacy Policy](PRIVACY.md)

簡單講：edEdit **完全不收集你的資料**。所有同步走 Apple 自家 iCloud，由你的 Apple ID 管理。

In short: edEdit collects **no data**. All sync goes through Apple's iCloud, managed by your Apple ID.

---

## 回報問題 · Issues

請走 [GitHub Issues](https://github.com/Adam1313943/edEdit-Public/issues)。
- 提交前請先看[既有 issue](https://github.com/Adam1313943/edEdit-Public/issues?q=is%3Aissue) 是否已被回報過
- 用 issue templates（Bug Report / Feature Request）能讓我快速處理

---

## 版本記錄 · Changelog

[CHANGELOG.md](CHANGELOG.md)

---

## 著作權 · Copyright

© 2026 momosoft. All rights reserved.

App 原始碼為私有專案，本 repo 僅作為說明文件、回報管道、與更新公告。
The app source code is proprietary; this repository serves only as documentation, issue tracking, and release notes.
