# OWASP Thick Client Application Security Verification Standard (TCASVS)

[![Downloads](https://img.shields.io/github/downloads/owasp/TCASVS/total?logo=github&logoColor=white&style=flat-square)](https://github.com/owasp/TCASVS/releases)
[![GitHub contributors](https://img.shields.io/github/contributors/owasp/TCASVS)](https://github.com/owasp/TCASVS/graphs/contributors)
[![GitHub issues](https://img.shields.io/github/issues/owasp/TCASVS)](https://github.com/owasp/TCASVS/issues)
[![GitHub pull requests](https://img.shields.io/github/issues-pr/owasp/TCASVS)](https://github.com/owasp/TCASVS/pulls)
[![CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-blue.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

## はじめに

OWASP Thick Client Application Security Verification Standard (TCASVS) は、シッククライアントアプリケーション (デスクトップソフトウェア、ネイティブアプリケーション、その他ブラウザのサンドボックス外で動作するローカル実行プログラム) を設計、構築、テストするための包括的なセキュリティ要件を提示します。

TCASVS はウェブアプリケーション向けの [OWASP Application Security Verification Standard (ASVS)](https://github.com/OWASP/ASVS) と [Mobile Application Security Verification Standard (MASVS)](https://github.com/OWASP/owasp-masvs) の間のギャップを埋めます。MASVS はシッククライアントのテストに適用できますが、最適なものではありません。TCASVS はシッククライアントのシナリオに特化して策定された標準を提供します。

## 最新安定版 — 5.0.0

標準のソースは [`5.0/ja/`](5.0/ja/) にあります。三つの検証レベルにわたる 130 以上のセキュリティ要件をカバーする 6 つの章を含みます。

| 章 | タイトル |
|----|----------|
| V1 | [アーキテクチャと脅威モデリング (Architecture and Threat Modeling)](5.0/ja/0x10-V1-Architecture-and-Threat-Modeling.md) |
| V2 | [構築、展開、環境の堅牢化 (Build, Deployment, and Environment Hardening)](5.0/ja/0x11-V2-Build-Deployment-and-Environment-Hardening.md) |
| V3 | [データストレージと保護 (Data Storage and Protection)](5.0/ja/0x12-V3-Data-Storage-and-Protection.md) |
| V4 | [コード品質とエクスプロイト軽減 (Code Quality and Exploit Mitigation)](5.0/ja/0x13-V4-Code-Quality-and-Exploit-Mitigation.md) |
| V5 | [暗号技術 (Cryptography)](5.0/ja/0x14-V5-Cryptography.md) |
| V6 | [ネットワーク通信 (Network Communication)](5.0/ja/0x15-V6-Network-Communication.md) |

## プロジェクトリーダーとワーキンググループ

本プロジェクトは [Dave Hanson](https://github.com/JeffreyShran) と [Samuel Aubert](https://github.com/matreurai) が主導し、Bentley Systems の AppSec チームの元メンバーおよび現メンバーである [Einaras Bartkus](https://github.com/eb-bsi), [Thomas Chauchefoin](https://www.linkedin.com/in/thomaschauchefoin), [John Cotter](https://www.linkedin.com/in/john-cotter-40338612/) が支援しています。

また、本プロジェクトは OWASP コミュニティおよび OWASP Foundation も支援しています。プロジェクトのディレクターとしての立場で支援いただいた [Starr Brown](https://github.com/mamicidal) に心から感謝します。

## 標準の目的

- 組織がシッククライアントアプリケーション向けの高品質なセキュアコーディングスタンダードを導入または適応することを支援します。
- アーキテクトや開発者が、セキュリティを設計および構築し、コントロールがあり、効果的であることを検証することで、セキュアなシッククライアントソフトウェアを構築することを支援します。
- セキュリティレビュー担当者が、シッククライアントのセキュリティ評価、コードレビュー、ペネトレーションテストにおいて、包括的で、一貫性のある、高品質な標準を使用することを支援します。
- シッククライアントアプリケーションのセキュリティの調達およびベンダー評価のためのフレームワークを提供します。

## 貢献

バグを見つけたり、アイデアがある場合には [issue を記録](https://github.com/OWASP/TCASVS/issues) してください。issue での議論に基づいたプルリクエストを歓迎します。

詳細な貢献ガイドラインについては [CONTRIBUTING.md](https://github.com/OWASP/TCASVS/blob/main/CONTRIBUTING.md) を参照してください。

## 貢献者

<a href="https://github.com/OWASP/TCASVS/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=OWASP/TCASVS" />
</a>

## Sponsors

<a href="https://www.bentley.com/company/about-us/">
  <div>
    <img src="images/BentleyLOGO_BLK_type.jpg" width="230" alt="Bentley Systems" />
  </div>
  <b>
    Bentley is the leading provider of infrastructure engineering software, advancing infrastructure for better quality of life and sustainability.
  </b>
  <div>
    <sup>Visit <u>bentley.com</u> to learn more.</sup>
  </div>
</a>

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=OWASP/TCASVS&type=Date)](https://star-history.com/#OWASP/TCASVS&Date)

## License

The entire project content is under the [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).

## Related Projects

- [OWASP Application Security Verification Standard (ASVS)](https://github.com/OWASP/ASVS)
- [OWASP Mobile Application Security Verification Standard (MASVS)](https://github.com/OWASP/owasp-masvs)
- [OWASP Software Assurance Maturity Model (SAMM)](https://github.com/OWASP/samm)
