# 常見問題 · FAQ

---

## 一般 · General

### Q: edEdit 是免費還是付費？

免費版能用 80% 功能（編輯任意檔案、5 筆筆記、Markdown 工具列、語法高亮、iCloud 同步、Share Extension 等）。Pro 一次買斷 USD $4.99 解鎖：

- 無筆記數量上限
- Find in Files（多檔搜尋）
- 檔案比較（Diff）
- 進階主題（陸續推出）

**沒有訂閱、沒有廣告、沒有追蹤。**

### Q: edEdit 為什麼不像其他 app 用訂閱？

我們相信買斷制更尊重 user。一次付清，未來新版本繼續可用。

### Q: 換新手機買的 Pro 還在嗎？

在。新手機裝 edEdit → 設定 → **還原購買** 即可。

### Q: 同個帳號的家人可以共用 Pro 嗎？

支援 Family Sharing（StoreKit 的 `familyShareable: true` 已啟用）。家人共享群組成員都能解鎖。

---

## 檔案編輯 · File Editing

### Q: 可以編輯哪些副檔名？

任意文字檔。內建語法高亮的有：Swift, JavaScript, TypeScript, Python, Go, Rust, C, C++, Java, Objective-C, Objective-C++, HTML, XML, JSON, YAML, Shell, Markdown, SQL, INI, Log。其他副檔名也能開，只是沒有語法高亮。

### Q: 支援的編碼？

UTF-8（含 BOM）、UTF-16（BE/LE）、Big5、GB2312、GB18030、Shift-JIS、ASCII。打開時自動偵測；存檔時保留原編碼。

### Q: 可以開很大的檔案嗎？

iOS 端目前沒有特別針對大檔做最佳化。macOS 端有 Tail mode 與 stream-load 機制，可開幾 GB 的 log 檔。

### Q: 編輯不小心存錯怎麼辦？

iOS 端目前沒有版本歷史。建議重要檔案放在 iCloud Drive — Apple 會保留 30 天版本歷史，可從 iCloud.com 還原。

---

## 筆記 · Notes

### Q: 筆記跟檔案差在哪？

**筆記**是 app 內部 Core Data，靠 CloudKit 同步，沒有副檔名概念，組織用標籤。**檔案**是磁碟上實體 `.md` / `.txt` 檔，用資料夾組織，可被其他 app 看到 / 編輯。

詳細看 [快速開始](getting-started.md)。

### Q: 筆記可以匯出成檔案嗎？

目前要手動 — 在筆記內選全部 → 複製 → 進「檔案」tab → 新建 `.md` → 貼上 → 存。

未來會加「匯出為檔案」直接動作。

### Q: 階層式標籤怎麼用？

底部 tag textfield 輸入 `work/meeting/2026Q1` — 用 `/` 自動分階層。側邊欄會顯示樹狀結構。

---

## iCloud 同步 · iCloud Sync

### Q: 同步要錢嗎？

不。用你 Apple ID 的 iCloud 5GB 免費空間就夠（筆記與小檔案佔很少）。

### Q: 我可以關掉 iCloud 同步嗎？

只能在系統設定 → Apple ID → iCloud → edEdit 那邊關。app 內沒有切換（受 Apple API 限制）。

### Q: iCloud 出問題怎麼辦？

看 [iCloud 同步說明 → Troubleshooting](icloud-sync.md#同步沒生效--troubleshooting)。

---

## 隱私 · Privacy

### Q: 我的資料會被收集嗎？

完全不會。edEdit 不裝任何 analytics / 廣告 / 追蹤 SDK，沒有 server 端，user 內容只存在你的裝置 + 你自己的 iCloud。

詳細看 [PRIVACY.md](../PRIVACY.md)。

### Q: 我可以把筆記與檔案完整匯出帶走嗎？

可以。
- **檔案**：本來就在你選的位置，直接從 Files app 拷貝走
- **筆記**：透過 iCloud Drive 看到的 `edEdit/` 資料夾包含 Pro 模式下的同步檔案；標準筆記可以一筆筆 copy 內容貼到外部編輯器

未來會加批次匯出功能。

---

## 平台 · Platforms

### Q: 有 macOS 版嗎？

有，跟 iOS 版功能對齊（含全部編輯、語法高亮、檔案比較、跨檔搜尋、Markdown 工具）。發行方式與定價待定。

### Q: 有 iPad 版嗎？

iOS app 是 Universal — 一個下載通用 iPhone 與 iPad。iPad 上 NavigationSplitView 自動展開三欄。

### Q: 有 Web 版 / Linux 版 / Windows 版嗎？

沒有，也不打算做。edEdit 強調「真正原生」 — 跨平台 web 框架與我們的 design philosophy 衝突。

---

## 其他 · Other

### Q: 我發現 bug / 想要新功能 / 翻譯有錯

歡迎到 [GitHub Issues](https://github.com/Adam1313943/edEdit-Public/issues) 開 issue。

### Q: 為什麼叫 edEdit？

「ed」是 Unix 經典文字編輯器；「Edit」就是編輯。簡短好記、念起來輕快。

### Q: 為什麼 Bundle ID 是 `com.momosoft.ezNotePadIOS`？

歷史包袱 — 早期叫 ezNotePad++，後來改名 edEdit 但 bundle ID 鎖定無法改（會破壞 user IAP）。
