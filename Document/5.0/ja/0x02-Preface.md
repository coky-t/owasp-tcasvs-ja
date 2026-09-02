# 序文

## TCASVS 5.0.0 へようこそ

OWASP Thick Client Application Security Verification Standard (TCASVS) は、シッククライアントアプリケーション (デスクトップソフトウェア、ネイティブアプリケーション、その他のブラウザサンドボックスの外で動作するローカル実行プログラム) の設計、開発、テストに関する包括的なセキュリティ要件を提示します。

本標準はウェブアプリケーション向けの [OWASP Application Security Verification Standard (ASVS)](https://github.com/OWASP/ASVS) と [Mobile Application Security Verification Standard (MASVS)](https://github.com/OWASP/owasp-masvs) との間のギャップを埋めるものです。これらの標準はそれぞれの領域を十分にカバーしていますが、シッククライアントアプリケーションは特有の脅威の組み合わせに直面しています。ユーザーが制御するハードウェア上で実行し、ローカルオペレーティングシステムリソースとやり取りし、信頼できないネットワーク経由で通信し、多くの場合、昇格された権限で動作します。

## TASVS からの変更点

TCASVS 5.0.0 は元来の Thick Application Security Verification Standard (TASVS) を全面的に再構築したものです。主な変更点は以下のとおりです。

- **要件 ID の形式**: 以前の `TASVS-{CATEGORY}-{group}.{item}` スキームを置き換え、ASVS ナンバリング (`V{chapter}.{section}.{item}`) を採用しました。
- **レベル定義**: 以前の X や空欄での表記を置き換え、単一の数値による `レベル` 列 (最低適用可能レベル) を使用して、要件ごとに L1/L2/L3 の適用を明確にしました。
- **CWE とのトレーサビリティ**: すべての要件は現在 CWE 識別子にマップしています。
- **カバレッジの拡張**: 以前の 79 要件から 6 章にわたる 130 以上になり、ビルドセキュリティ、メモリ安全性、IPC、ランタイム完全性に対する重要な補完を伴います。
- **章の再構成**: シッククライアント特有の脅威を残しつつ、ASVS の慣行に準拠した章立てに再編しました。
- **バージョンの整合**: OWASP ASVS 5.0.0 に合わせてバージョン番号 `5.0.0` を採用しました。TCASVS が ASVS の形式、構成、公開パイラインを共有していることを示すものです。この共通のバージョン付けは、TASVS 1.0 と本標準との段階的なリリースであることを主張するものではなく、意図的に整合を選択したものです。

## 章の構成

| 章 | タイトル | 焦点 |
|----|----------|------|
| V1 | アーキテクチャと脅威モデリング (Architecture and Threat Modeling) | 脅威モデル、セキュリティアーキテクチャ、攻撃対象領域管理 |
| V2 | 構築、展開、環境の堅牢化 (Build, Deployment, and Environment Hardening) | サプライチェーン、コンパイラ緩和策、インストーラ、権限管理 |
| V3 | データストレージと保護 (Data Storage and Protection) | データ分類、ファイルストレージ、クレデンシャル、メモリ、一時データ |
| V4 | コード品質とエクスプロイト軽減 (Code Quality and Exploit Mitigation) | 入力バリデーション、メモリ安全性、デシリアライゼーション、ランタイム完全性 |
| V5 | 暗号技術 (Cryptography) | アルゴリズム、鍵管理、乱数、通信の暗号化 |
| V6 | ネットワーク通信 (Network Communication) | TLS、サービス公開、データ漏洩、IPC、ライセンスバリデーション |

## セキュリティ検証レベル

TCASVS は以下の三つの検証レベルを定義しています。

- **レベル 1 (L1)** — すべてのシッククライアントアプリケーションに適した基本的なセキュリティです。これらの要件は最も一般的かつ容易に悪用できる脆弱性を対処します。
- **レベル 2 (L2)** — 機密データを扱うアプリケーションや、よりリスクの高い環境で運用するアプリケーションのための標準的なセキュリティです。多層防御策を含み、より高度な能力を持つ敵対者を想定します。
- **レベル 3 (L3)** — 敵対的な環境で運用するアプリケーション、より機密性の高いデータを扱うアプリケーション、あるいは物理的なアクセスやリバースエンジニアリング能力を持つ熟練した敵対者による標的型攻撃への耐性を要するアプリケーションのための高度なセキュリティです。

## 本標準の使い方

The TCASVS can be used as:

1. **A development guide** — Requirements inform secure design decisions during architecture and implementation.
2. **A verification checklist** — Security testers use requirements as test cases during assessments.
3. **A procurement specification** — Organizations include TCASVS compliance in vendor security requirements.
4. **A maturity benchmark** — Teams assess their current security posture against defined levels and plan improvements.

Select the appropriate level based on the application's risk profile, then verify all requirements at that level and below are met.
