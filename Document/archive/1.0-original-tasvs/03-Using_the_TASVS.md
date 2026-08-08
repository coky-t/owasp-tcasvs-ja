# シッククライアントアプリケーションセキュリティ検証標準

この検証標準は以下を行おうとする人に役に立つでしょう。

- 安全なアプリケーションの開発と保守
- アプリケーションのセキュリティの評価


## シッククライアントアプリケーションセキュリティモデル

本標準は `TASVS-{word}` というラベルの付いたさまざまなグループに分かれており、シッククライアント攻撃対象領域の最も重量な領域を表しています。これらのコントロールグループは `TASVS-{word}-{digit}` というラベルの付いたサブグループに分かれています。これらの各コントロールグループは `TASVS-{word}-{digit}.{digit}` というラベルの付いた個別のコントロールを含んでおり、標準を満たすために実装する必要がある特定のセキュリティ対策に関するガイダンスを提供します。たとえば `TASVS-ARCH-1.1` です。

### トップグループ

- TASVS-ARCH - アーキテクチャと脅威モデリング (Architecture & Threat Modelling)
- TASVS-CODE - コード品質とエクスプロイト軽減 (Code Quality and Exploit Mitigation)
- TASVS-CONF - 構成と構築 (Configuration and Building)
- TASVS-CRYPTO - 暗号 (Cryptography)
- TASVS-NETWORK - 通信とプライバシー (Communication and Privacy)
- TASVS-STORAGE - データストレージ (Data Storage)
- TASVS-FUTURE - Coming soon General considerations for future cloud adoption strategies.

### サブグループ

- TASVS-ARCH-1 - 脅威モデリング (Threat Modeling)
- TASVS-CODE-1 - サーバーサイド (Server Side)
- TASVS-CODE-2 - クライアントサイド - 署名と完全性 (Client Side - Signing and Integrity)
- TASVS-CODE-3 - クライアントサイド - 静的コード解析 (Client Side - Static Code Analysis)
- TASVS-CODE-4 - クライアントサイド - バリデーション、サニタイゼーション、エンコーディング (Client Side - Validation, Sanitization and Encoding)
- TASVS-CODE-5 - クライアントサイド - ビジネスロジック (Client Side - Business Logic)
- TASVS-CODE-6 - クライアントサイド - ファジング (Client Side - Fuzzing)
- TASVS-CODE-7 - クライアントサイド - セキュアコーディングプラクティス (Client Side - Secure Coding Practices)
- TASVS-CONF-1 - 一般的な構成チェック (General Configuration Checks)
- TASVS-CONF-2 - 権限とパーミッション (Privileges and Permissions)
- TASVS-CRYPTO-1 - 通信 (Communication)
- TASVS-CRYPTO-2 - ストレージ (Storage)
- TASVS-CRYPTO-3 - 全般 (General)
- TASVS-NETWORK-1 - データ漏洩 (Data leakage)
- TASVS-NETWORK-2 - ライセンスと認証サーバー (Licensing & Authentication Servers)
- TASVS-NETWORK-3 - 海賊版の検出 (Piracy Detection)
- TASVS-NETWORK-4 - コネクテッドサービス (Connected Services)
- TASVS-STORAGE-1 - 機密情報レビュー (Sensitive Information Review)
- TASVS-STORAGE-2 - DLL ハイジャッキング (DLL Hijacking)


## アプリケーションセキュリティ検証レベル

私たちは [Web Application Security Verification Standard](https://github.com/OWASP/ASVS/tree/master) と同じレベル分け方法論に従います。三つの検証レベルを定義し、レベルごとに深さが増していきます。

- L1 - TASVS レベル 1 は低補償レベルであり、ペネトレーションテストを通じて完全に検証可能です。
- L2 - TASVS レベル 2 は機密データを含むアプリケーション向けであり、保護が必要であり、ほとんどのアプリで推奨されるレベルです。
- L3 - TASVS レベル 3 は最も重要なアプリケーション向けであり、機密性の高い医療データなどの高価値のトランザクションを処理するアプリケーションや最高レベルの信頼性を必要とするアプリケーションを対象としています。



\newpage{}
