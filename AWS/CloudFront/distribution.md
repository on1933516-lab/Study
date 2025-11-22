# CloudFront ディストリビューション設定

　Flutter Web（S3）＋ API Gateway 構成

---

## 1. オリジン（Origin）

CloudFront が **どこからファイルを取得するか** を定義する項目。

### ● shared-expense-app の構成では：
- **Origin Domain**：S3 バケット（Origin Access Control）
- **Origin Path**：空（指定なし）

CloudFront はここで指定した S3 から  
`index.html` / `main.dart.js` / `assets/...` を取得して返す。

---

## 2. Default Root Object

CloudFront が **ルート（https://xxxxx.cloudfront.net/）へアクセスされたときに返すファイル** を指定する。

### ● shared-expense-app の場合：
 index.html

---

## 3. サポートされている HTTP バージョン

使用できるプロトコルは以下の通り：

- HTTP/2  
- HTTP/1.1  
- HTTP/1.0

※ HTTP/3 について  
HTTP/3 は HTTP/2 の次世代プロトコルで、QUIC（UDPベース）を使うため  
**接続が速く、不安定な通信でも強い** という特徴がある。

CloudFront も HTTP/3 をサポートしているが、  
**利用者側（ブラウザ）の対応状況によって自動的に切り替わる方式のため、  
特別な設定は不要で、通常は HTTP/2 。**

---

##### ■すべてのディストリビューション設定リファレンス
https://docs.aws.amazon.com/ja_jp/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html#DownloadDistValuesPathPattern

##### ■shared-expense-app
https://github.com/on1933516-lab/shared-expense-app/tree/main
