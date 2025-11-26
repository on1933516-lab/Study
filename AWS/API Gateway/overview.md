# API Gatewayについて

## API Gatewayの概要

API の作成・管理・セキュリティをフルマネージドで提供する AWSサービス。

サーバー管理が不要で、“どのリクエストをどのバックエンド（Lambda など）に渡すか” を制御するゲートウェイの役割を担う。

 - スケーラブル
 - 認証・認可（IAM / Cognito）と統合
 - トラフィック管理（スロットリング：一度に大量のリクエストが来た場合に対処できるよう、リクエスト数を制限する）
 - CORS（他ドメインからのアクセス制御）、WAFとの連携
 - CloudWatch でのログ・メトリクス管理

---
引用：

##### ■ Amazon API Gateway

##### https://aws.amazon.com/jp/api-gateway/

##### ■ Choose between REST APIs and HTTP APIs

##### https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html

---

### ● shared-expense-app の場合：

API Gateway を API の統合ポイント（リクエストの受け取り口） として利用し、
以下のように HTTP リクエストを Lambdaへルーティングしている。

```
GET /expenses → lambda_get_expenses
POST /expenses → lambda_add_expense
PUT /expenses/{id} → lambda_update_expense
DELETE /expenses/{id} → lambda_delete_expense
```
#### 特記事項

 - プロトコル：HTTP（REST APIの機能が不要なため、低コストなHTTP APIを選択）
 - IP アドレスのタイプ：IPv4（国内利用を想定したテスト的システムのため、デフォルトの IPv4 を選択）
 - CORS 有効化（Flutter Web対応のため）
 - 認証は現時点では実装なし
 - API Gateway と Lambda 間は IAM ロールでセキュアに接続
