# 序文

## TCASVS 5.0.0 へようこそ

OWASP Thick Client Application Security Verification Standard (TCASVS) は、シッククライアントアプリケーション (デスクトップソフトウェア、ネイティブアプリケーション、その他のブラウザサンドボックスの外で動作するローカル実行プログラム) の設計、開発、テストに関する包括的なセキュリティ要件を提示します。

本標準はウェブアプリケーション向けの [OWASP Application Security Verification Standard (ASVS)](https://github.com/OWASP/ASVS) と [Mobile Application Security Verification Standard (MASVS)](https://github.com/OWASP/owasp-masvs) との間のギャップを埋めるものです。これらの標準はそれぞれの領域を十分にカバーしていますが、シッククライアントアプリケーションは特有の脅威の組み合わせに直面しています。ユーザーが制御するハードウェア上で実行し、ローカルオペレーティングシステムリソースとやり取りし、信頼できないネットワーク経由で通信し、多くの場合、昇格された権限で動作します。

## TASVS からの変更点

TCASVS 5.0.0 represents a complete restructuring of the original Thick Application Security Verification Standard (TASVS). Key changes include:

- **Requirement ID format**: Adopted ASVS numbering (`V{chapter}.{section}.{item}`) replacing the old `TASVS-{CATEGORY}-{group}.{item}` scheme.
- **Level definitions**: Clarified L1/L2/L3 applicability per requirement using a single numeric `Level` column (the lowest applicable level), replacing the old X/blank notation.
- **CWE traceability**: Every requirement now maps to a CWE identifier.
- **Expanded coverage**: From 79 original requirements to over 130 across 6 chapters, with significant gap-fills for build security, memory safety, IPC, and runtime integrity.
- **Chapter restructuring**: Reorganized into chapters that align with ASVS conventions while remaining specific to thick client threats.
- **Version alignment**: Adopted the `5.0.0` version number to mirror OWASP ASVS 5.0.0, signalling that TCASVS shares its format, structure, and publishing pipeline. This co-versioning is a deliberate alignment choice rather than a claim of incremental releases between TASVS 1.0 and this standard.

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
