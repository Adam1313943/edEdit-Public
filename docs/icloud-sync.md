# iCloud 同步 · iCloud Sync

edEdit 用 Apple 自家的 iCloud 跨裝置同步，**不經過任何第三方伺服器**。

edEdit syncs across devices via Apple's iCloud — **not through any third-party servers**.

---

## 同步什麼 · What Syncs

| 項目 | 同步方式 |
|---|---|
| **筆記**（Notes tab 內）| **CloudKit**（透過 `NSPersistentCloudKitContainer`）— 自動、即時 |
| **iCloud Drive 資料夾的檔案** | **iCloud Drive** — Apple 內建，跟其他 iCloud Drive 檔案一樣 |
| **本機檔案 / 第三方雲端的檔案** | ❌ 不同步（檔案就在你選的位置）|
| **App 設定（Pro 購買狀態）** | App Store / StoreKit 帳號層級，自動同步 |

---

## 怎麼開啟 · How to Enable

iOS：
1. 設定 app → Apple ID → iCloud → **iCloud Drive 開啟**
2. 往下捲找到 **edEdit**，確認**開關已開**
3. 開 edEdit → 進「檔案」tab → 應該看到「iCloud · edEdit」section

iOS:
1. Settings → Apple ID → iCloud → enable **iCloud Drive**
2. Scroll down to **edEdit** and ensure its toggle is on
3. Open edEdit → Files tab → you should see the "iCloud · edEdit" section

macOS：
1. 系統設定 → Apple ID → iCloud → **iCloud Drive 開啟**
2. 確認 edEdit 在清單內並啟用

---

## edEdit 在 iCloud Drive 中的資料夾 · The "edEdit" Folder

當你開啟 app 並登入 iCloud，edEdit 會在 iCloud Drive 自動建立 **`edEdit/`** 資料夾。

When you launch the app while signed into iCloud, edEdit automatically creates an **`edEdit/`** folder in iCloud Drive.

- 在 iPhone：Files app → 瀏覽 → iCloud Drive → edEdit
- 在 Mac：Finder → 側邊欄 iCloud Drive → edEdit
- 在 web：iCloud.com → iCloud Drive → edEdit

你存到這裡的檔案會跟其他 iCloud Drive 內容一樣**自動跨裝置同步**。

Files saved here sync automatically across devices like any other iCloud Drive content.

---

## 同步衝突怎麼辦 · Sync Conflicts

iCloud 用 Apple 的 NSFileCoordinator + 內建衝突處理。如果兩台裝置同時改同一個檔案 / 同一筆筆記：

iCloud uses Apple's NSFileCoordinator with built-in conflict resolution. If two devices edit the same file or note simultaneously:

- **檔案**：可能保留兩個版本（檔名後加「(衝突版本 from iPhone)」之類），打開 Files app 可看到
- **筆記**：CloudKit 會合併或讓最後寫入的版本勝出（last-writer-wins）

實務上很少遇到，因為 Apple 的同步速度通常 < 1 秒。

In practice this is rare since Apple syncs in under a second.

---

## 同步沒生效？ · Troubleshooting

| 症狀 | 解法 |
|---|---|
| Files app 看不到 edEdit 資料夾 | 進設定 → Apple ID → iCloud → 確認 iCloud Drive 開、且 edEdit 切換為開 |
| 一台裝置編輯了但另一台沒同步 | 重啟兩台裝置的 edEdit；確認都登入同一個 Apple ID |
| 一直顯示「載入中」 | 檢查網路；iCloud Drive 在弱網環境會延遲幾分鐘 |
| 筆記在 iPad 看不到（但 iPhone 有）| 第一次同步可能要等 1-2 分鐘；之後即時 |
| 完全不想用 iCloud | App 設定無法關閉 CloudKit（Apple API 限制），但你可以在系統設定 → Apple ID → iCloud → edEdit 關閉，筆記就只存本機 |

---

## 隱私 · Privacy

iCloud 的內容**只屬於你**。Apple 不能讀（end-to-end 對於部分資料；筆記是 standard）；momosoft 完全看不到。

詳細請看 [Apple iCloud Privacy](https://www.apple.com/icloud/) 與我們的 [PRIVACY.md](../PRIVACY.md)。
