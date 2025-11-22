# CloudFront のキャッシュの仕組み

CloudFront は、利用者に近いエッジロケーションにファイルをキャッシュすることで  
高速なレスポンスを実現している。

ただし、Flutter Web のような静的ファイル（main.dart.js など）は  
**CloudFront・ブラウザ・ServiceWorker の3段階で強力にキャッシュされるため、更新が反映されにくい**  
というデメリットもある。

→ その場合は **Invalidation** によってキャッシュを削除して解決できる。


# Invalidation（キャッシュ削除）

S3 のファイルを変更しても、CloudFront が古いキャッシュを返すことがある。

そのため、変更を即時反映させたい場合は CloudFront の  
**「Create invalidation」** 機能を使い、特定のオブジェクトパスのキャッシュを削除する。

例：  
- `/*` → 全ファイルのキャッシュを削除  
- `/main.dart.js` → JS のみ削除  
- `/assets/*` → 画像・CSS など特定ディレクトリだけ削除

削除後は、CloudFront が S3 に最新ファイルを取りにいくため、  
画面に変更が反映されるようになる。


##### ■ CloudFront – Invalidation の公式説明

##### https://docs.aws.amazon.com/ja_jp/AmazonCloudFront/latest/DeveloperGuide/Invalidation.html

