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

| Chapter | Title | Focus |
|---------|-------|-------|
| V1 | Architecture and Threat Modeling | Threat models, security architecture, attack surface management |
| V2 | Build, Deployment, and Environment Hardening | Supply chain, compiler mitigations, installers, privilege management |
| V3 | Data Storage and Protection | Data classification, file storage, credentials, memory, temp data |
| V4 | Code Quality and Exploit Mitigation | Input validation, memory safety, deserialization, runtime integrity |
| V5 | Cryptography | Algorithms, key management, random values, transport crypto |
| V6 | Network Communication | TLS, service exposure, data leakage, IPC, license validation |

## セキュリティ検証レベル

The TCASVS defines three verification levels:

- **Level 1 (L1)** — Baseline security appropriate for all thick client applications. These requirements address the most common and easily exploitable weaknesses.
- **Level 2 (L2)** — Standard security for applications that handle sensitive data or operate in higher-risk environments. Includes defense-in-depth measures and assumes a more capable adversary.
- **Level 3 (L3)** — Advanced security for applications operating in hostile environments, handling highly sensitive data, or requiring resistance to targeted attacks by skilled adversaries with physical access and reverse engineering capabilities.

## 本標準の使い方

The TCASVS can be used as:

1. **A development guide** — Requirements inform secure design decisions during architecture and implementation.
2. **A verification checklist** — Security testers use requirements as test cases during assessments.
3. **A procurement specification** — Organizations include TCASVS compliance in vendor security requirements.
4. **A maturity benchmark** — Teams assess their current security posture against defined levels and plan improvements.

Select the appropriate level based on the application's risk profile, then verify all requirements at that level and below are met.
