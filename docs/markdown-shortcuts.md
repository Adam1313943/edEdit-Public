# Markdown 編輯快速鍵 · Markdown Shortcuts

edEdit 在編輯 `.md` 檔或筆記時提供豐富的 Markdown 編輯輔助。

When editing a `.md` file or note, edEdit provides rich Markdown editing assistance.

---

## 鍵盤上方工具列 · Keyboard Accessory Bar (iOS)

開啟 .md 檔或編輯筆記時，鍵盤上方會出現一排格式按鈕：

When editing a Markdown file or note, a toolbar appears above the keyboard:

| 圖示 | 功能 |
|---|---|
| H | 標題（單擊放第 1 級、再點放第 2 級）/ Heading levels |
| **B** | 粗體 / Bold |
| *I* | 斜體 / Italic |
| S̶ | 刪除線 / Strikethrough |
| `</>` | 行內程式碼 / Inline code |
| • | 項目符號清單 / Bullet list |
| 1. | 有序清單 / Ordered list |
| ☑ | 待辦清單 / Task list |
| ❝ | 引用 / Blockquote |
| 🔗 | 連結 / Link |
| 🖼 | 圖片 / Image |

---

## 硬體鍵盤快速鍵 · Hardware Keyboard Shortcuts

接外接鍵盤或在 macOS 編輯時可用：

When using an external keyboard or on macOS:

| 動作 / Action | 快速鍵 / Shortcut |
|---|---|
| 粗體 / Bold | ⌘B |
| 斜體 / Italic | ⌘I |
| 行內程式碼 / Inline code | ⌘E |
| 連結 / Link | ⌘K |
| 圖片 / Image (macOS) | ⇧⌘K |
| 刪除線 / Strikethrough (macOS) | ⇧⌘S |
| 標題 1-6 / Heading 1-6 | ⌘1 ～ ⌘6 |

---

## 智慧自動行為 · Smart Behaviour

### 清單續行 · List continuation

在以下行末按 Enter，自動續一個項目：

Press Enter at the end of any of these lines to auto-continue:

```markdown
- 項目              ← Enter 後自動加 "- "
1. 編號項目         ← Enter 後自動加 "2. "
- [ ] 待辦         ← Enter 後自動加 "- [ ] "
> 引用             ← Enter 後自動加 "> "
```

### 跳出清單 · Exit list

如果某個清單項目是**空的**（只有 `- ` 沒有內容），按 Enter 自動跳出清單。

If a list item is empty (just `- ` with no content), pressing Enter exits the list.

---

## 剪貼簿圖片貼進 .md · Paste Images into Markdown

1. 截圖或複製圖片到剪貼簿
2. 在 .md 檔內按 ⌘V（或長按貼上）
3. edEdit 智慧處理：
   - **檔案有存到磁碟（known location）** → 圖片寫成 `<basename>-img-N.png` 放在原檔旁邊，插入 `![](filename.png)` 引用
   - **檔案還沒存** → 用 base64 data URI 內嵌 `![](data:image/png;base64,...)`

兩種情況產出的 .md 都是有效的 Markdown，任意 viewer / 編輯器打開都能正常顯示。

---

## Apple Notes 格式自動轉換 · Auto-convert from Apple Notes

從 iOS 內建 Notes 透過 Share → edEdit 進來的內容，會自動將：

When sharing from Apple Notes via Share → edEdit, formatting auto-converts:

| Notes 格式 | edEdit 看到的 Markdown |
|---|---|
| **粗體文字** | `**粗體文字**` |
| *斜體* | `*斜體*` |
| 標題（大字）| `# 標題` |
| • 項目 | `- 項目` |
| ☐ 待辦 | `- [ ] 待辦` |
| ☑ 已完成 | `- [x] 已完成` |
| [連結](url) | `[連結](url)` |

底層用 `NSAttributedString` 直接解析 RTF/RTFD 屬性，**不會**經過任何雲端服務。

Under the hood we parse RTF/RTFD via NSAttributedString locally — no cloud service involved.
