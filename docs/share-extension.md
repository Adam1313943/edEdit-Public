# 從備忘錄分享 · Sharing from Apple Notes

edEdit 註冊為 iOS 系統 Share Extension，從任何 app 的「分享」按鈕都能把內容帶進來。

edEdit registers as a system Share Extension — content from any app's "Share" button can be brought into edEdit.

---

## 流程 · Flow

1. 在 Apple Notes（或其他 app）按 **分享** 按鈕
2. 在分享面板找到 **edEdit**（如果沒看到，往下滑找「**更多**」/「More」加上勾選）
3. 點下去出現一個 mini-UI：

```
┌─ 取消 ─── 儲存到 edEdit ─── 下一步 ─┐
│                                      │
│ 檔名                                 │
│ ┌───────────────────────────┐        │
│ │ Untitled                  │        │
│ └───────────────────────────┘        │
│                                      │
│ 格式                                 │
│ ⊙ ★ 存為 edEdit 筆記（預設）          │
│ ○ Markdown (.md)                    │
│ ○ 單一 HTML（含內嵌圖片）             │
│ ○ 純文字 (.txt)                     │
│                                      │
│ 預覽                                 │
│ ─────────────────────────────────   │
│ # 我的筆記內容                       │
│ - 項目一                             │
│ - 項目二                             │
│ ...                                  │
└──────────────────────────────────────┘
```

---

## 4 種儲存方式 · Four Save Options

### 1. ⭐ 存為 edEdit 筆記（預設）· Save as edEdit Note

不會建立檔案；內容直接進入「筆記」tab，跟你在 app 內手動建的筆記一樣。圖片以 base64 內嵌進筆記內容。

No file is created; content goes straight into the Notes tab, identical to a note you'd create inside the app. Images are inlined as base64.

### 2. Markdown (.md)

存成標準 `.md` 檔；如果原始分享內容有附圖片，圖片會以**獨立檔案**存放在同一資料夾，`.md` 內用 `![](filename.png)` 引用。

Saves as a standard `.md` file. Attached images go into the same folder as separate files, referenced with `![](filename.png)`.

### 3. 單一 HTML（含內嵌圖片）· Single HTML

存成單一 `.html` 檔，圖片用 base64 data URI 內嵌，整個檔案完全自包含、適合分享。

Saves as a single `.html` with images base64-inlined. Fully self-contained, ideal for sharing.

### 4. 純文字 (.txt)

只保留文字，剝除所有格式。

Plain text only, all formatting stripped.

---

## 格式自動轉換 · Automatic Format Conversion

從 Apple Notes 進來的 RTF / RTFD 內容會自動解析並轉換：

RTF / RTFD content from Apple Notes is automatically parsed and converted:

| Apple Notes | edEdit 看到的 |
|---|---|
| **粗體文字** | `**粗體文字**` |
| *斜體* | `*斜體*` |
| 大字標題 | `# 標題` |
| 中字標題 | `## 標題` |
| • 項目一 | `- 項目一` |
| 1. 第一點 | `1. 第一點` |
| ☐ 待辦 | `- [ ] 待辦` |
| ☑ 已做 | `- [x] 已做` |
| [連結文字](https://...) | `[連結文字](https://...)` |
| 等寬文字 | `` `等寬文字` `` |

### 不會被轉的 · Not Converted

- 字型大小、顏色 — Markdown 沒這個概念
- 手寫塗鴉 — 略過
- 表格（如果 Notes 有用到）— 退成純文字
- 附加的 Apple Notes 簽名（pencil 簽名）— 略過

---

## 跨裝置 · Cross-Device

從 Mac 的 Notes 分享同樣能用 — 但 Mac 沒有 edEdit Share Extension，要走另一條路：

1. Mac Notes → 全選文字 → 複製
2. 開 edEdit → 新建檔案 / 筆記 → 貼上

未來可能加 Mac 版 Share Extension（透過 NSSharingService）。

A Mac Share Extension may be added in a future version.

---

## App Group 設定 · App Group Setup

edEdit 用 App Group 在 Share Extension 與主 app 間傳資料。如果你看到「App Group 共享空間還沒設定」錯誤，表示安裝有異常 — 請[回報](https://github.com/Adam1313943/edEdit-Public/issues)。

If you see an "App Group container is not configured" error, please [file an issue](https://github.com/Adam1313943/edEdit-Public/issues).

---

## 隱私 · Privacy

Share Extension 的內容傳遞**完全在裝置本機**進行：

- 文字 / 圖片從 Notes app 透過 iOS 系統 NSItemProvider 機制傳給 edEdit Share Extension
- 「存為筆記」走 App Group 共享資料夾傳給主 app
- **完全不經過任何網路 / 雲端**

Content transfer happens entirely on-device — no network or cloud involved.
