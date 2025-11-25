# バケットポリシーについて

S3のアクセス制御は通常「バケット単位」で設定するが、  
**バケットポリシー(Bucket Policy)** を活用すると、  
「誰が・どのオブジェクトに・何を実行できるか」まで詳細に制御できる。

---

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowPutObjectS3ServerAccessLogsPolicy",
      "Principal": {
        "Service": "logging.s3.amazonaws.com"
      },
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::amzn-s3-demo-bucket-logs/*",
      "Condition": {
        "StringEquals": {
          "aws:SourceAccount": "111122223333"
        },
        "ArnLike": {
          "aws:SourceArn": "arn:aws:s3:::amzn-s3-demo-source-bucket1"
        }
      }
    },
    {
      "Sid": "RestrictToS3ServerAccessLogs",
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::amzn-s3-demo-bucket-logs/*",
      "Condition": {
        "ForAllValues:StringNotEquals": {
          "aws:PrincipalServiceNamesList": "logging.s3.amazonaws.com"
        }
      }
    }
  ]
}
```

### 項目概要
- **Version**：IAMポリシーの書式バージョン。
- **Statement**：付与する権限や条件を記述する。ステートメントブロックで複数記述可能。
- **ステートメントブロック**：｛｝で囲まれた範囲のこと。制御する権限と条件を記述する。
- **Sid**：ユーザーがバケットポリシーに付与できる識別子。
- **Effect**：actionの内容を許可/拒否するかを記述する。
- **Principal**：バケットへアクセス可能なリソースまたはユーザーを指定する。（*でAWSアカウントが無い場合もアクセス可となる）
- **Action**：制御したい操作を記述する。

引用：AWSの基本・仕組み・重要用語が全部わかる教科書

### ● shared-expense-app の場合：

CloudFront 経由のみでオブジェクト取得できるように設定している。
(CloudFront からのアクセスのみに限定することで、
S3 バケットをパブリックにせずに静的ファイルを配信でき、セキュリティを確保できる。)
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowCloudFrontServicePrincipal",
            "Effect": "Allow",
            "Principal": {
                "Service": "cloudfront.amazonaws.com"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::${bucketName}/*",
            "Condition": {
                "ArnLike": {
                    "AWS:SourceArn": "arn:aws:cloudfront::xxxxxxxxxx:distribution/XXXXXXXXXXXXX"
                }
            }
        }
    ]
}
```
