# 發版檢查清單 · Release Checklist

每次發布 edEdit 前照這份清單操作，避免重蹈覆轍。維護者用。

Run through this before every edEdit release. Maintainer-facing.

---

## 0. 發版前 · Before You Start

- [ ] 所有要發的變更都已 merge 到 `main`
- [ ] 本機 build 乾淨（macOS + iOS 都能 archive，無 warning 爆量）
- [ ] 決定版號：`CFBundleShortVersionString`（顯示版號）+ `CFBundleVersion`（build number，**每次上傳都要遞增**）

---

## 1. CloudKit Schema（**只有改過 `NoteModel.xcdatamodeld` 才需要**）

筆記功能用 `NSPersistentCloudKitContainer`。**Development 環境會自動建 schema，Production 不會** —— production 一定要手動部署，否則用戶建立筆記時雲端寫入會以 `CKErrorDomain` code 2（partialFailure）失敗。

- [ ] 用 Xcode Debug build 跑過一次（讓 development 環境自動建好新 schema）
- [ ] 開 [icloud.developer.apple.com](https://icloud.developer.apple.com/) → container `iCloud.com.momosoft.edEdit`
- [ ] **Schema → Development** → 確認 `CD_CDNote`、`CD_CDTag` 及新增的欄位都在
- [ ] 按 **Deploy Schema Changes to Production** → 確認變更清單 → Deploy
- [ ] 等 1–2 分鐘讓 production 生效

> ⚠️ Production schema **只能加、不能改名/刪**。要移除欄位只能 Reset Production Environment（會清空所有真實用戶資料）。所以 model 改動永遠用「新增」，舊欄位留著當 deprecated。
>
> ⚠️ 順序很重要：**先 deploy schema，再放 app 出去**。反過來的話，用戶更新後到你 deploy 之間會 sync 失敗。

純 code / UI / bug fix（沒動 `.xcdatamodeld`）→ **跳過這整節**。

---

## 2. macOS 發版

### 2a. Build / 簽署 / 公證

- [ ] Xcode → macOS scheme → Archive
- [ ] Distribute → Developer ID → 簽署 + 上傳 Apple 公證 + staple
- [ ] 把成品 `.app` 放到 `~/Downloads/edEdit.app`
- [ ] 確認 entitlements 正確：
  ```
  codesign -d --entitlements :- ~/Downloads/edEdit.app
  ```
  應該看到 `aps-environment = production`、`icloud-services` 含 `CloudKit`、`icloud-container-environment = Production`

### 2b. 打包 + 發 GitHub Release

- [ ] 在私有 repo 跑 `Scripts/release-dmg.sh`（會自動讀版號、打 dmg、開 GitHub Release）
  - 同版號修正想覆蓋 → `gh release upload v<X> edEdit-<X>.dmg --repo Adam1313943/edEdit-Public --clobber`
- [ ] 確認 release 頁的 `.dmg` 大小 / 時間正確
- [ ] 更新 `release-notes.md`（私有 repo 根目錄），下次發版直接覆寫

---

## 3. iOS 發版

- [ ] Xcode → iOS scheme → Generic iOS Device → Archive
- [ ] Organizer → Distribute App → App Store Connect → Upload
- [ ] App Store Connect → TestFlight → 等 processing
- [ ] **In-App Purchase 狀態確認**：營收 → App 內購買項目 → `edEdit Pro` 必須是 **「已核准 / Approved」**
  - 第一次發 IAP：要把 IAP 綁到該 app 版本一起送審，否則 IAP 會永遠卡在「準備提交」，價格看得到但買不了
- [ ] 送 App Store 審查 → 上架

---

## 4. 發版後驗證 · Post-Release Smoke Test

- [ ] iOS 從 App Store 下載正式版（production 環境）
- [ ] macOS 用簽署過的 dmg 安裝（production 環境）
- [ ] 任一台建一筆筆記 → 等 30 秒～2 分鐘 → 另一台應該看得到（驗證 CloudKit production 同步）
- [ ] 測試 Pro 購買流程（用沒買過的 sandbox / 正式帳號）

---

## 環境對照表 · Environment Matrix

CloudKit 同步**只在相同環境之間**運作。dev-signed app 跟 App-Store app 連的是**不同的 CloudKit 資料庫**。

| App 來源 | CloudKit 環境 |
|---|---|
| Xcode Run（Debug）| **development** |
| TestFlight | **production** |
| App Store | **production** |
| Developer ID 簽署 dmg | **production** |

開發期間 → 三台都用 Xcode Run（全 development，不用 deploy schema）。
驗證正式環境 → 全部 TestFlight / App Store / 簽署 dmg（全 production，schema 要先 deploy 過）。

---

## IAP 促銷碼注意事項 · IAP Promo Codes

- **生效延遲**：促銷碼產生後要等 **15 分鐘～數小時**才會在 Apple 系統全面生效，剛產生就兌換常回「無效」
- **有效期**：生效後 **28 天**到期
- **數量**：每個 app（含所有 IAP）每版本共 **100 組**
- **兌換前提**：IAP 促銷碼 ≠ app 促銷碼 —— **必須先安裝正式版 app**，再兌換（建議用 App Store Connect 給的 URL，比手動輸入穩）
- **帳號**：entitlement 掛在「媒體與購買項目」帳號，跟 iCloud 帳號無關；edEdit 查 entitlement 也是查同一個帳號，所以兩者不同帳號**不影響**兌換

---

## 踩過的坑 · Lessons Learned

| 症狀 | 真正原因 |
|---|---|
| 筆記在 dev build 之間同步 OK，正式版不同步 | Production schema 沒 deploy |
| 換到正式版後看不到 dev 建的筆記 | dev / production 是兩個獨立資料庫，Apple 設計上不互通、不遷移 |
| CloudKit Console 看不到任何資料 | Console 顯示的是**你開發者 Apple ID 對應的 iCloud 帳號**的 private database；若跟裝置上的 iCloud 帳號不同就看不到（這是隱私設計，正常）|
| 內購促銷碼「無法使用」 | 多半是促銷碼還沒生效（剛產生），或 app 不是 App Store 正式版 |
