# V1 アーキテクチャと脅威モデリング (Architecture and Threat Modeling)

## 管理目標

シッククライアントアプリケーションは極めて過酷な環境で動作します。エンドユーザーが制御するハードウェア上で実行し、信頼できないネットワークを介して通信し、ローカルのオペレーティングシステムリソースとやり取りし、多くの場合、昇格した権限で動作します。ブラウザのサンドボックスに制限されるウェブアプリケーションとは異なり、シッククライアントは、ローカルファイルシステム、プロセス間通信、カーネルインタフェース、ネットワークエンドポイントにわたる、広範かつ多様な攻撃対象領域をさらします。構造化された脅威モデルと意図的なアーキテクチャセキュリティ設計なしでは、チームはこのデプロイメントモデルに特有のリスクを体系的に特定し、優先順位付けし、緩和することができません。この章では、シッククライアントアプリケーションがセキュリティを最優先のアーキテクチャ上の課題として設計され、脅威が開発ライフサイクル全体を通じて特定および追跡され、バイナリ改竄、メモリ操作、権限昇格といったクライアント特有のベクトルを含む、攻撃対象領域全体が文書化および管理されることを確保します。

## V1.1 脅威モデルの文書化 (Threat Model Documentation)

脅威モデルは、文書化され、アクセス可能であり、セキュリティ判断を導くために十分具体的である場合にのみ役立ちます。シッククライアントアプリケーションでは、脅威モデルは、サーバーのみのアーキテクチャに存在しない攻撃対象領域 (ローカルストレージ、IPC メカニズム、OS レベルインタラクション) と、攻撃者がクライアントバイナリに物理的に完全にアクセスできるという現実を考慮に入れる必要があります。これらの要件は、脅威モデルが存在し、アプリケーションのリスクレベルに応じた適切な詳細さを備え、シッククライアントのデプロイメント全体をカバーすることを確保します。

| # | 説明 | レベル | ソース |
|---|------|:------:|--------|
| V1.1.1 | 脅威モデルがシッククライアントアプリケーションに対して存在しており、少なくともアプリケーションのエントリポイント、資産、信頼境界、およびクライアントサイド、サーバーサイド、ネットワーク、ローカルの攻撃対象領域に関する高レベルの脅威を特定していることを検証します。 | 1 | TASVS |
| V1.1.2 | 詳細な脅威モデルが本番アプリケーションに対して維持されており、データフロー図、各コンポーネントに対する STRIDE または同等の脅威分類、リスク評価済みの脅威シナリオと文書化された緩和策を含むことを検証します。 | 2 | TASVS |
| V1.1.3 | 脅威モデルのスコープが、すべてのサーバーサイドコンポーネント、サードパーティの依存関係、クラウドサービスとの統合 (API、OIDC プロバイダ、ファイルストレージ)、クライアントとサーバー間の通信チャネルを明示的に含むことを検証します。 | 2 | TASVS |
| V1.1.4 | 脅威モデルアーティファクトがアプリケーションコードとともにソースコードリポジトリに格納され、バージョン管理され、標準的な変更プロセスの一環としてレビュー可能であることを検証します。 | 1 | TASVS |
| V1.1.5 | 脅威モデルがアプリケーション内のすべての信頼境界を文書化しており、ユーザーモードコンポーネントとカーネルモードコンポーネント間の境界、異なる権限レベルのプロセス間の境界、クライアントアプリケーションとバックエンドサービス間の境界を含むことを検証します。 | 2 | New |
| V1.1.6 | データフロー図が、機密データ (クレデンシャル、トークン、PII、ビジネス上重要なデータ) が信頼境界を渡るすべての経路を特定し、各通過点に適用される保護メカニズムを文書化していることを検証します。 | 2 | New |

## V1.2 脅威モデリングのプロセス (Threat Modeling Process)

Creating a threat model once and filing it away provides little ongoing value. Thick client applications evolve rapidly — new features expose new IPC channels, dependency updates introduce new attack surface, and architectural changes shift trust boundaries. These requirements ensure that threat modeling is a living process integrated into the secure development lifecycle, not a one-time compliance exercise.

| # | 説明 | レベル | ソース |
|---|------|:------:|--------|
| V1.2.1 | Verify that the threat modeling process encompasses all phases: system modeling (architecture decomposition), automated threat identification (tooling-assisted), manual threat identification (expert review), and threat mitigation planning with assigned owners. | 2 | TASVS |
| V1.2.2 | Verify that the threat model is reviewed and updated at defined intervals and upon significant architectural changes, as part of the development team's documented secure development lifecycle (SSDLC). | 2 | TASVS |
| V1.2.3 | Verify that the threat model is validated against the implemented application by confirming that documented mitigations are present and effective, and that no undocumented attack surfaces exist. | 3 | New |
| V1.2.4 | Verify that threat modeling outputs are used as input for security test planning, with each identified threat having at least one corresponding test case or verification activity. | 2 | New |

## V1.3 アーキテクチャセキュリティ設計 (Architecture Security Design)

Thick clients face architectural challenges that server-side applications do not: they must manage privilege separation across local processes, isolate plugin subsystems that run untrusted code, secure their own update mechanisms against tampering, and sometimes operate in adversarial environments where the local OS itself cannot be trusted. These requirements ensure that security is designed into the architecture rather than bolted on after deployment.

| # | 説明 | レベル | ソース |
|---|------|:------:|--------|
| V1.3.1 | Verify that architecture documentation describes the privilege separation model, including which components run at elevated privilege, what IPC mechanisms connect them, and how the principle of least privilege is applied to each process. | 1 | New |
| V1.3.2 | Verify that the architecture documents security design principles applied to the thick client, including defense in depth, fail-secure defaults, complete mediation, and economy of mechanism. | 2 | New |
| V1.3.3 | Verify that the architecture documents how plugin, extension, or scripting subsystems are isolated from the host application, including what APIs are exposed, what permissions are required, and how malicious plugins are prevented from accessing privileged functionality. | 2 | New |
| V1.3.4 | Verify that the architecture documents the application's update and patching mechanism design, including the trust chain for update verification, rollback capabilities, and how partial or failed updates are handled securely. | 2 | New |
| V1.3.5 | Verify that the architecture documents how the application handles execution in an adversarial local environment where the OS, other processes, and the user may be hostile (e.g., anti-cheat, DRM, or security-sensitive applications). | 3 | New |

## V1.4 攻撃対象領域管理 (Attack Surface Management)

Thick clients expose attack surface across multiple dimensions simultaneously: local filesystem paths, registry keys, named pipes, shared memory, COM objects, listening network ports, outbound connections, and user-facing input vectors. Unlike server applications where the attack surface is primarily network-facing, thick clients must defend against local attackers with debugger access, binary analysis tools, and the ability to inject code into the process. These requirements ensure the full attack surface is identified, documented, and actively managed as the application evolves.

| # | 説明 | レベル | ソース |
|---|------|:------:|--------|
| V1.4.1 | Verify that the application's attack surface is documented, including all local interfaces (filesystem paths, registry keys, named pipes, shared memory, COM objects), network interfaces (listening ports, outbound connections), and user-facing input vectors. | 1 | New |
| V1.4.2 | Verify that the attack surface documentation identifies which interfaces are exposed to unauthenticated or low-privilege callers, and that each such interface has documented input validation and access control expectations. | 2 | New |
| V1.4.3 | Verify that the threat model explicitly addresses thick-client-specific attack vectors, including binary reverse engineering, memory tampering, local privilege escalation, DLL/dylib injection, debugger attachment, and inter-process communication abuse. | 1 | New |
| V1.4.4 | Verify that attack surface changes introduced by new features or dependency updates are assessed and the threat model is updated before deployment to production. | 2 | New |

## 参考情報

- [OWASP Threat Modeling](https://owasp.org/www-community/Threat_Modeling)
- [OWASP Threat Modeling Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Threat_Modeling_Cheat_Sheet.html)
- [Microsoft STRIDE Threat Model](https://learn.microsoft.com/en-us/azure/security/develop/threat-modeling-tool-threats)
- [OWASP Attack Surface Analysis Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Attack_Surface_Analysis_Cheat_Sheet.html)
