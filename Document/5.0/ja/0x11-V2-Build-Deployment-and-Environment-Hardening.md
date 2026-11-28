# V2 構築、展開、環境の堅牢化 (Build, Deployment, and Environment Hardening)

## 管理目標

シッククライアントアプリケーションは、不要な攻撃対象領域を排除し、利用可能なプラットフォームセキュリティ機能を活用するような形で構築、パッケージ化、デプロイ、構成されるようにします。この章では、サプライチェーンの完全性、コンパイラレベルのエクスプロイト緩和、安全なインストールおよびアップデートのメカニズム、実行時権限の最小化をカバーします。

## V2.1 ビルドとサプライチェーンのセキュリティ (Build and Supply Chain Security)

このセクションはビルドパイプラインとサードパーティ依存関係の完全性を取り扱い、製品アーティファクトが信頼でき、最小限であり、追跡可能であることを確保します。

| # | 説明 | レベル | ソース |
|---|------|:------:|--------|
| V2.1.1 | アプリケーションのビルドおよびデプロイメントのプロセスが、完全性保護されたビルド環境を備えた CI/CD パイプラインを使用して自動化されており、再現可能なアーティファクトを生成することを検証します。 | 1 | TASVS |
| V2.1.2 | アプリケーションおよびすべての依存関係が、自動化されたスクリプトから再デプロイできること、あるいは文書化された復旧時間枠内にバックアップから復元できることを検証します。 | 2 | TASVS |
| V2.1.3 | 製品ビルドが、すべての不要な機能、サンプルコード、ドキュメント、テストユーティリティ、開発設定を除外していることを検証します。 | 1 | TASVS |
| V2.1.4 | すべてのサードパーティコンポーネントが、事前定義され、信頼でき、継続的に保守されているリポジトリから取得されており、ダウンロードされたアーティファクトの完全性検証していることを検証します。 | 1 | TASVS |
| V2.1.5 | ソフトウェア部品表 (SBOM) が、推移的依存関係を含む、使用しているすべてのサードパーティライブラリについて維持されており、リリースごとに更新されていることを検証します。 | 1 | TASVS |
| V2.1.6 | 製品ビルドが、デバッグシンボル、詳細なエラー文字列、開発者クレデンシャルの埋め込みを含まないこと検証します。 | 1 | New |
| V2.1.7 | リリースされるバイナリおよびインストーラが適切で有効期間内にある証明書を用いてコード署名されていること、および、署名鍵がハードウェア (HSM または同等のもの) によって保護されていることを検証します。 | 2 | New |
| V2.1.8 | ビルドシステムが、依存関係を完全性ハッシュでピン留めし、内部パッケージに対してプライベートレジストリを優先的に使用することで、依存関係混乱攻撃から保護されていることを検証します。 | 2 | New |

## V2.2 環境の堅牢化 (Environment Hardening)

This section covers compiler and OS-level exploit mitigations that must be enabled in production builds to raise the cost of memory corruption exploitation.

| # | 説明 | レベル | ソース |
|---|------|:------:|--------|
| V2.2.1 | Verify that compiler and linker flags enable all available exploit mitigations, including stack canaries, stack randomization, and data execution prevention, and that the build fails on unsafe pointer, memory, format string, integer, or string operations. | 1 | TASVS |
| V2.2.2 | Verify that the application binary enables Address Space Layout Randomization (ASLR) by being compiled as a position-independent executable (PIE) with a high-entropy base address. | 1 | New |
| V2.2.3 | Verify that Data Execution Prevention (DEP/NX) is enforced for all executable modules, preventing code execution from data segments. | 1 | New |
| V2.2.4 | Verify that Control Flow Integrity (CFI) protections are enabled where supported by the compiler toolchain, such as Control Flow Guard (CFG) on Windows or CFI on Clang/LLVM. | 2 | New |
| V2.2.5 | Verify that hardware-assisted exploit mitigations (such as Intel CET shadow stacks or ARM PAC/BTI) are enabled for builds targeting platforms that support them. | 3 | New |
| V2.2.6 | Verify that the application does not disable or weaken OS-level security features at runtime (e.g., calling SetProcessDEPPolicy to disable DEP, marking memory as RWX without justification). | 2 | New |

## V2.3 インストールとアップデートのセキュリティ (Installation and Update Security)

This section ensures that installers and auto-update mechanisms cannot be subverted to deliver tampered code or escalate privileges beyond what is necessary.

| # | 説明 | レベル | ソース |
|---|------|:------:|--------|
| V2.3.1 | Verify that the installer validates its own integrity before execution (e.g., embedded signature verification or checksum validation from a trusted manifest). | 1 | New |
| V2.3.2 | Verify that the installer does not create temporary files with insecure permissions in world-writable directories, or that such files are integrity-checked before use. | 1 | New |
| V2.3.3 | Verify that the application's auto-update mechanism validates cryptographic signatures on update packages before applying them, using a trust anchor independent of the downloaded package. | 1 | New |
| V2.3.4 | Verify that the auto-update mechanism uses TLS with certificate pinning or equivalent for update downloads, and fails closed if verification fails. | 2 | New |
| V2.3.5 | Verify that the installer and application use safe DLL search order and do not load libraries from user-writable or uncontrolled directories, preventing DLL sideloading and search-order hijacking. | 1 | New |
| V2.3.6 | Verify that installer privilege elevation (e.g., UAC prompts on Windows) is limited to the minimum operations that require elevated privileges, and that elevated child processes are not exposed to untrusted input. | 2 | New |

## V2.4 特権とパーミッションの管理 (Privilege and Permission Management)

This section addresses runtime privilege minimization, process isolation, and proper access control on filesystem and IPC objects created by the application.

| # | 説明 | レベル | ソース |
|---|------|:------:|--------|
| V2.4.1 | Verify that the application runs with the minimum privileges required for its functionality, and that elevated components expose only the minimum necessary IPC interface surface. | 1 | TASVS |
| V2.4.2 | Verify that the application satisfies the "Rule of 2": it does not simultaneously process untrustworthy input, use a memory-unsafe language, and run with elevated privileges or without a sandbox. | 1 | TASVS |
| V2.4.3 | Verify that filesystem permissions are correctly restricted on all directories and files created, modified, or accessed during installation and at runtime, preventing unauthorized read, write, or execute access by lower-privileged users. | 1 | TASVS |
| V2.4.4 | Verify that Windows services or system daemons used by the application run under dedicated service accounts with minimal privileges, not as LocalSystem, root, or equivalent unless explicitly justified and documented. | 2 | New |
| V2.4.5 | Verify that configuration files, registry keys, and local databases used by the application are protected with restrictive ACLs preventing modification by non-administrative users. | 1 | New |
| V2.4.6 | Verify that the application implements sandboxing or process isolation for components that handle untrusted input (e.g., file parsers, protocol handlers, plugin hosts), limiting access to the filesystem, network, and system APIs. | 2 | New |
| V2.4.7 | Verify that named pipes, shared memory segments, and other OS IPC objects created by the application use restrictive security descriptors that prevent connection or modification by unauthorized processes. | 2 | New |

## 参考情報

- [OWASP ASVS 5.0.0](https://github.com/OWASP/ASVS)
- [CWE/SANS Top 25](https://cwe.mitre.org/top25/)
- [Microsoft Security Development Lifecycle](https://www.microsoft.com/en-us/securityengineering/sdl)
- [NIST SP 800-218 - Secure Software Development Framework](https://csrc.nist.gov/publications/detail/sp/800-218/final)
- [SLSA Supply Chain Levels for Software Artifacts](https://slsa.dev/)
