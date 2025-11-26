# WAFについて

## WAFの概要

AWSが提供するWebアプリケーションファイアウォール。


代表的な用途
 - アプリケーションの脆弱性を悪用した攻撃の遮断(SQL インジェクション, XSS)
 - アプリケーション層の DDoS 対策
 - 不正なボットによるアクセスの遮断

WAFのデプロイ可能なサービス
 - CloudFront
 - API Gateway
 - ALB

---
引用：

##### ■ AWS WAF とは

##### https://aws.amazon.com/jp/waf/what-is-waf/

---

### ● shared-expense-app の場合

本アプリでは、**CloudFront ディストリビューションに WAF を関連付け**、  
特定 IP 以外のアクセスをブロックするルールを設定している。

アプリが個人用のプロトタイプであるため、  
**許可リスト（Allow-list）方式** を採用し、  
管理者（自宅ネットワーク）からのアクセスのみ許可している。


### 適用ルール

#### **Default Action: BLOCK**  
　Allow で明示的に許可された場合のみアクセスを通す。

#### **Rule Priority（評価順序）**
　- Allow（許可ルール） → 最優先で評価  
　- Default Block → 最後に実行されるフェイルセーフ  

---

### ● 特記事項（適用中の個別ルールセット）

#### **IP Allow/Block Rule**
- 自宅 Wi-Fi（固定 IP）のみ許可  
- その他の IP はすべてブロック  
  （`0.0.0.0/1` + `128.0.0.0/1` で IPv4 全体をカバー。IPv6 も同様に 2 分割で設定）

#### **GlobalRateBasedRule（Count モード）**
　短時間で大量リクエストを送ってくる相手を検知するルール。  
　※Count モードのため検知のみでブロックはしない。

#### **BodySizeRestrictionRule（Count モード）**
　想定より大きすぎるリクエストボディを検知するルール。  
　※Count モードのため監視目的。

#### **AWS-AWSManagedRulesCommonRuleSet**
　XSS、コマンドインジェクションなど OWASP Top 10 に含まれる一般的な攻撃を防御。

#### **AWS-AWSManagedRulesSQLiRuleSet**
　SQL インジェクション攻撃をブロック。

#### **AWS-AWSManagedRulesAdminProtectionRuleSet**
　`/admin`、`/wp-login`、`/phpmyadmin` など管理系パスへの攻撃をブロックするルール。
