# Firebase 登入與雲端同步設定

不設定也能用：`index.html` 最上方的 `FB` 設定留空，就是單機模式（不用登入，資料只存在該瀏覽器）。

## 一、建立 Firebase 專案
1. 到 https://console.firebase.google.com 建立專案（不需要 Google Analytics）。
2. 專案首頁按「</>」新增網頁應用程式，取名後會看到 `firebaseConfig`。
3. 把 `apiKey`、`authDomain`、`projectId`、`appId` 貼進 `index.html` 裡的 `var FB={...}`。
   - 這組設定不是密碼，公開在網頁上是正常的；真正的保護靠第四步的規則。

## 二、開啟登入方式
Authentication → 登入方式 → 啟用「Google」，需要帳號密碼登入的話也啟用「電子郵件/密碼」。
- 電子郵件/密碼的帳號，請到 Authentication → 使用者 → 新增使用者，由你自己建立。
- 若你的帳號設定有「允許自行註冊」的選項，請關閉。

Authentication → 設定 → 已授權網域，加入 `你的帳號.github.io`。

## 三、建立資料庫
Firestore Database → 建立資料庫 → 選「正式版模式」，地區可選 asia-east1（台灣）。

## 四、貼上安全規則（最重要）
1. 先用你的帳號登入一次網頁（這時會顯示權限不足，正常）。
2. Authentication → 使用者，複製你那一列的「使用者 UID」。
3. 把 `firestore.rules` 裡的內容貼到 Firestore → 規則，把 UID 換成真的，按發布。
4. 要讓同事使用，請同事登入一次，把他的 UID 也加進名單。

## 注意
- 資料存在 Firestore 的單一文件，上限約 1 MB（大約兩三千筆證照）。
- 兩個人同時修改時，後存的人會被提醒「別人剛更新了資料」，需先載入最新版再重做。
- 登出時會清掉這台電腦上的本機快取。
- 免費方案（Spark）夠用。
