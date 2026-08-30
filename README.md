# PikPak WebDAV 連線設定完整教學：怎麼開啟？服務器地址怎麼填？RaiDrive、Infuse、VidHub 全平台配置一次搞定（附最新會員方案對比表）

好，我要先說一個讓我有點難為情的往事。

大概兩年前，我在 PikPak 裡存了差不多快兩個 TB 的影片。那時候每次想看，我的操作流程是：打開 PikPak → 找到檔案 → 點下載 → 等它下到本地 → 再用播放器打開。

對，就這樣。我就這樣用了很久，從來沒覺得有什麼不對。

後來有個朋友問我有沒有設 WebDAV，我說什麼是 WebDAV，他的表情讓我感覺自己像剛從洞裡爬出來的人。

然後他示範給我看——打開 Infuse，直接串流 PikPak 裡的 4K 影片，不用下載，不用等，就像用 Netflix 一樣。

從那天開始，我就跟「先下載再看」的時代說再見了。

這篇文章，就是把我自己踩坑、摸索出來的 PikPak WebDAV 連線設定流程，完整寫給你看。

---

## **PikPak WebDAV 是什麼？跟你有什麼關係？**

先簡單解釋一下 WebDAV 這個東西。

WebDAV 是一種基於 HTTP 的網路協議，全名是 Web Distributed Authoring and Versioning。聽起來很技術，但本質很簡單：它讓你可以透過網路，像操作本地資料夾一樣存取和管理遠端伺服器上的檔案。

PikPak 官方支援 WebDAV 協議。這意味著，只要你啟用這個功能，任何支援 WebDAV 的客戶端軟體——Windows 的 RaiDrive、iOS 的 Infuse、Apple TV 的 VidHub、NAS 上的 rclone——都可以直接連進你的 PikPak 雲端硬碟，不用透過 PikPak 官方客戶端。

**透過 PikPak WebDAV，你可以做到：**

- 用第三方播放器（Infuse、VidHub、Kodi）直接串流 PikPak 裡的影片
- 把 PikPak 掛載成 Windows 或 macOS 的本地磁碟盤符
- 透過 rclone 整合進 NAS 媒體管理流程
- 複製、移動、重新命名、上傳、下載所有檔案

**目前不支援的操作：**

- 永久刪除檔案（只能移入回收站）
- 清空回收站

還有一件事要先說清楚，因為很多人踩過這個坑：**PikPak WebDAV 連線設定是 Premium 會員專屬功能**，免費帳號沒有辦法使用。如果你還是免費版，後面的設定步驟對你來說都是空談。

> 還沒升級？ 👉 [點這裡查看 PikPak Premium 會員方案](https://bit.ly/PIkpak)

---

## **第一步：在 PikPak 啟用 WebDAV 並取得憑證**

### **網頁版入口（最新版本推薦）**

1. 登入 PikPak 網頁版
2. 前往「**設定 > 存取與整合 > WebDAV**」
3. 點擊啟用 WebDAV
4. 建立 WebDAV 憑證
5. 頁面上會顯示三個關鍵資訊：
   - **伺服器地址（Server URL）**
   - **使用者名稱（Username）**
   - **密碼（Password）**

把這三個資訊記下來，或截圖保存，後面所有平台的連線設定都要填這些。

### **PC 桌面客戶端入口（舊版）**

如果你用的是 PikPak PC 桌面版，舊版的入口位置稍有不同：

1. 打開 PikPak PC 客戶端
2. 進入「**設定 > 實驗室功能 > WebDAV**」
3. 開啟 WebDAV 開關，查看連接憑證

> ⚠️ **重要提醒**：WebDAV 憑證是系統為你獨立生成的，跟你平時登入 PikPak 的帳號密碼**完全不同**。不要把它分享給任何人，也不要跟別人共用帳號——PikPak 有帳號共享偵測機制，被抓到可能直接停服 24 小時。

所有生成的 WebDAV 憑證可以在「**帳號與安全 > 已連線的應用**」裡查看、管理或刪除。

---

## **PikPak WebDAV 連線資訊一覽**

在填入任何客戶端之前，先把這張表存起來：

| 欄位 | 資訊 |
| --- | --- |
| **伺服器地址** | `dav.mypikpak.com` |
| **協議** | HTTPS |
| **Port** | `443`（HTTPS）/ `80`（HTTP） |
| **使用者名稱** | PikPak 設定頁面顯示的 WebDAV 使用者名稱 |
| **密碼** | PikPak 設定頁面顯示的 WebDAV 密碼 |

---

## **各平台 PikPak WebDAV 連線設定步驟**

### **Windows 電腦：用 RaiDrive 掛載為本地磁碟**

RaiDrive 是 Windows 上最流行的 WebDAV 掛載工具之一，設定完成後 PikPak 會直接出現在「本機」裡，像 D 槽、E 槽一樣，拖拖拉拉、播放影片，完全沒有違和感。

**設定步驟：**

1. 下載並安裝 RaiDrive（官網搜尋 RaiDrive 下載）
2. 打開 RaiDrive，點「**添加**」
3. 連接類型選「**NAS > WebDAV**」
4. 填入連線資訊：
   - 伺服器地址：`dav.mypikpak.com`
   - Port：`443`
   - 使用者名稱：你的 PikPak WebDAV 使用者名稱
   - 密碼：你的 PikPak WebDAV 密碼
5. 其他選項保持預設，點「**連接**」

連接成功後，打開「本機」，你就會看到 PikPak 以一個新磁碟的形式出現。播影片、整理檔案，跟操作本地硬碟幾乎沒有區別。

> 💡 有一個現實要說：WebDAV 的速度完全取決於你本地網路連接 PikPak 伺服器的品質。網路好的話，體驗非常絲滑；如果你本來訪問 PikPak 就不穩定，這個問題 WebDAV 也解決不了。

---

### **iOS / Apple TV：在 Infuse 裡添加 PikPak**

Infuse 是很多人 Apple 生態看片的第一選擇，原生支援 WebDAV，跟 PikPak 的組合幾乎是目前串流雲端影片最順暢的方案之一。

**設定步驟：**

1. 打開 Infuse，進入「**設定 > 文件 > 添加文件源**」
2. 選擇「**WebDAV**」
3. 填入：
   - 地址：`dav.mypikpak.com`
   - Port：`443`
   - 使用者名稱 & 密碼：PikPak WebDAV 憑證
4. 儲存

儲存完成後，Infuse 會自動掃描你的 PikPak 影片庫，杜比視界、HDR10、藍光原盤，想看什麼直接點。

---

### **iOS / Apple TV：用 VidHub 直連 PikPak**

VidHub 是近幾年快速崛起的播放器，功能強大、免費版就很好用，同樣原生支援 WebDAV。

**設定步驟：**

1. 打開 VidHub，點「**添加文件源 > 添加 WebDAV**」
2. 填入：
   - **名稱**：隨意填，例如「PikPak」
   - **協議**：HTTP 或 HTTPS 均可
   - **伺服器地址**：複製 PikPak 設定頁面的統一連接地址
   - **Port**：HTTP 填 `80`，HTTPS 填 `443`
   - **使用者名稱 & 密碼**：PikPak WebDAV 憑證
   - **路徑**：可以不填
3. 點「**儲存**」

幾秒後你的 PikPak 就掛載完成，可以直接在 VidHub 裡瀏覽和播放所有影片。

---

### **NAS / Linux / macOS：rclone 指令行掛載**

如果你有 NAS，或者喜歡用指令行工具，rclone 是最靈活的方案，可以把 PikPak 掛載到任意路徑，甚至做雙向同步。

**設定範例：**

bash
# 執行 rclone 設定向導
rclone config

# 選擇 webdav
# URL 填寫：https://dav.mypikpak.com
# Vendor 選擇 other
# 輸入使用者名稱和密碼


掛載指令：

bash
rclone mount pikpak: /mnt/pikpak --vfs-cache-mode writes


---

### **進階方案：透過 Alist / OpenList 整合**

如果你想把 PikPak 整合進 Emby、Jellyfin，或者同時管理多個雲端硬碟，可以先把 PikPak 掛載到 Alist / OpenList，再透過這些工具的 WebDAV 介面統一對外輸出。

這個方案設定稍微複雜一點，但對於有 NAS 的用戶來說，靈活性和可管理性都要強很多。Alist 的 PikPak 掛載設定中，WebDAV 策略建議選擇「302 重定向」，這樣串流時不會讓所有流量都走 Alist 中轉，速度更快。

---

## **PikPak 全套餐方案對比（含 WebDAV 權限）**

說了這麼多設定，最後來把會員方案也理清楚。

PikPak 的會員分**全球版（Global）** 和**區域版（Regional）** 兩種，主要差異是下載速度上限和適用地區。台灣、香港、澳門、東南亞大多數地區都屬於**區域會員**範疇，價格比全球版便宜不少。

### **全球會員 vs 區域會員主要差異**

| 特性 | 全球會員 | 區域會員 |
| --- | --- | --- |
| 適用地區 | 美、加、日、韓、德、法、英等 33 國 | 其他國家地區 |
| 最高下載速度 | 20 MB/s（全球不限地區） | 8 MB/s（到全球會員地區會限速） |
| 儲存空間 | 10 TB | 10 TB |
| WebDAV 支援 | ✅ Premium 專屬 | ✅ Premium 專屬 |
| 離線下載次數 | 無限制 | 無限制 |
| 4K 線上播放 | ✅ | ✅ |

### **完整套餐價格對比表**

| 套餐方案 | 儲存空間 | 計費週期 | 參考價格 | 購買連結 |
| --- | --- | --- | --- | --- |
| **免費版** | 6 GB | 永久免費 | $0 | [免費開始使用](https://bit.ly/PIkpak) |
| **Premium 月付（區域）** | 10 TB | 每月自動續費 | 約 US$5.79/月 | [訂閱月付方案](https://mypikpak.com/drive/payment?invitation-code=74098243) |
| **Premium 年付（區域）** | 10 TB | 每年一次性付款 | 約 US$57.59/年（等於約 US$4.8/月） | [訂閱年付方案](https://mypikpak.com/drive/payment?invitation-code=74098243) |
| **Premium 月付（全球）** | 10 TB | 每月自動續費 | 約 US$9.49/月 | [訂閱全球月付](https://mypikpak.com/drive/payment?invitation-code=74098243) |
| **Premium 年付（全球）** | 10 TB | 每年一次性付款 | 約 US$63.99/年（等於約 US$5.33/月） | [訂閱全球年付](https://mypikpak.com/drive/payment?invitation-code=74098243) |

> 📌 **小提醒**：年付方案比月付划算很多——以區域會員為例，年付折算每月大約 US$4.8，比月付省了接近 17%。如果你打算長期使用 PikPak（WebDAV、離線下載、串流一起用），年付是明顯更合算的選擇。

> ⚠️ 以上價格為參考數字，實際金額以 PikPak 官方購買頁面顯示為準，不同地區可能略有差異。

支援的付款方式包括信用卡、PayPal、加密貨幣、支付寶、銀聯等，方式挺多的，基本上怎麼方便怎麼付。

---

## **WebDAV 連線常見問題解答**

**Q：我是 Premium 會員，但找不到 WebDAV 設定選項？**

確認一下你使用的是最新版本的 PikPak 客戶端或網頁版。入口位置在「設定 > 存取與整合 > WebDAV」（新版）或「設定 > 實驗室功能 > WebDAV」（舊版桌面端）。如果還是找不到，可以嘗試切換到網頁版操作。

**Q：WebDAV 憑證生成後，去哪裡查看和管理？**

前往「**帳號與安全 > 已連線的應用**」，每個生成的 WebDAV 憑證都會列在這裡，你可以查看活動記錄，或者隨時刪除不需要的憑證。

**Q：連上 WebDAV 但速度很慢怎麼辦？**

WebDAV 的速度本質是受限於你本地網路連接 PikPak 伺服器的品質。幾個可以嘗試的方向：確認你的網路對 PikPak 訪問是否穩定；如果你用的是某些限速明顯的運營商（例如中國移動），可能需要搭配其他網路方案；或者考慮在 PikPak 裡直接離線存取，速度通常更快。

**Q：不同客戶端有沒有相容性問題？**

PikPak 官方也明確說過，各個 WebDAV 客戶端的實現方式不同，確實可能出現相容性問題。遇到問題可以換個客戶端試試，或者向 PikPak 客服反饋。整體來說，RaiDrive、Infuse、VidHub 這幾個的相容性都還不錯。

**Q：WebDAV 可以讓多台裝置同時連線嗎？**

可以。你可以在不同裝置上填入同一組 WebDAV 憑證同時使用。但要注意，**PikPak 禁止帳號共享**，不要把憑證給不同使用者使用，那會觸發帳號共享偵測。

---

## **最後說幾句**

PikPak WebDAV 這個功能，說白了就是把雲端硬碟的使用方式從「下載後用」升級成「即時用」。對於影片黨、NAS 用戶、Apple TV 播放器使用者來說，這個改變是質的飛躍。

10 TB 的儲存空間，配上 WebDAV 直連串流，再加上 PikPak 原本就很強悍的離線存取能力——整個體驗拼起來，比很多貴得多的方案都要好用。

區域年付方案折算下來每個月不到五塊美金，說實話這個定價對於這些功能來說，相當有誠意。

如果你一直在猶豫要不要升級，這篇文章或許可以幫你下定決心。

👉 [點這裡查看 PikPak 最新會員方案與優惠](https://bit.ly/PIkpak)
