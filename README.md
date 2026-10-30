# 名合 貴洋｜ソフトウェアエンジニア

**ポートフォリオ：** https://art-full-stack.com/

C/C++による産業機器の制御ソフトウェアや画像処理・外観検査システムの開発と、React・Go・Laravelを用いたWebアプリケーション開発に取り組んでいます。

直近の実務では、Tauri（React, Rust）を用いた外観検査装置向けアプリケーションで、制御プログラムとUIの両方を担当し、課題の把握から機能検討・設計・実装・テストまで対応しています。

個人開発では、C++の画像処理技術とWeb技術の連携に加え、Go・gRPCによるAPI開発、Dockerを用いたサービス構成、AWSへのデプロイ・監視まで取り組んでいます。技術単体だけでなく、各コンポーネントを連携させてアプリケーション全体を構築することを重視しています。

## 技術スタック

- **言語：** C, C++, Python, Go, PHP, Rust, TypeScript
- **フロントエンド：** React, Vue.js, Vite, WebAssembly, Web Worker, Tailwind CSS
- **バックエンド・API：** Go REST API, gRPC, Protocol Buffers, Laravel, MySQL, OpenAI API
- **デスクトップ：** Tauri
- **画像処理：** OpenCV
- **インフラ・運用：** Linux（Rocky Linux 9）, Docker / Docker Compose, AWS（EC2, Systems Manager, CloudWatch, SNS）, Nginx, Cloudflare Pages
- **開発ツール：** Git, GitHub, GitHub Actions

## 実務経験

- C/C++による産業機器の制御プログラム開発・機能改修
- C++・画像処理を用いた外観検査システムの開発
- Tauri（Rust, Vue.js, React, TypeScript)を用いたデスクトップアプリケーションの開発
- 課題の把握から設計、実装、テストまでの一貫した開発
- Linux・Dockerを用いた開発環境での業務経験

## 個人開発

### [SVG App](https://github.com/TakahiroNago/svg-app) / [Webフロントエンド](https://github.com/TakahiroNago/svg-web) / [デモ（ブラウザ内変換）](https://svg.art-full-stack.com/) / [AWS版（サーバー側変換）](https://aws-svg.art-full-stack.com/)

ラスター画像をSVGに変換するWebアプリケーションです。C++20とOpenCVで実装した変換エンジンを、ブラウザ内のWebAssemblyと、Go REST APIからgRPC経由で呼び出すサーバー側の、2つの経路から利用できる構成にしています。

- C++20・OpenCVによる減色（Lab色空間でのk-means）、輪郭抽出、SVG生成
- 変換コアをCLIから分離し、WebAssemblyとgRPCサーバーで共通利用
- React・TypeScriptによるWebインターフェースと、Web Workerによる変換処理
- Go REST APIとC++ gRPCサーバーの連携、Protocol Buffersによるサービス定義
- AWS EC2上でのDocker Composeによるサービス管理と、NginxによるHTTPS終端
- Cloudflare Pagesでのブラウザ内変換版の公開
- GitHub ActionsによるCI（proto・Go・C++・統合テスト）と、AWS Systems Manager経由の自動デプロイ
- CloudWatchによるEC2監視と、SNSによるメール通知

**2つの変換経路**

- ブラウザ内変換：`React / TypeScript → Web Worker → WebAssembly → C++ / OpenCV`
- サーバー側変換：`React / TypeScript → Nginx → Go REST API → gRPC → C++ / OpenCV`

### [PaintMix](https://github.com/TakahiroNago/paint-mix-app) / [デモ](https://paint.art-full-stack.com/)

絵の具の混色をシミュレーションするWebアプリケーションです。

- React・TypeScriptによるUI設計と型安全な実装
- Mixboxを利用した混色処理
- 日本語・英語のUI
- 混色処理と画面のテスト

### [ZEN — 心の庵](https://github.com/TakahiroNago/zen-app) / [デモ](https://zen.art-full-stack.com/ja)

禅の考え方を参考にしたAI相談アプリケーションです。Laravel・PHPで、企画・設計・実装から、テスト、本番環境へのデプロイ・運用まで一貫して開発しています。

- OpenAI APIとの連携と、応答方針を制御するプロンプト設計
- 過去の相談のトピック分類・要約を活用した対話
- 個人情報と思われる記述の検出と、伏せ字の提案
- Stripe決済の導入と、Webhook・契約状態の管理
- Googleログイン、日本語・英語のUI
- GitHub Actionsによるテスト・ビルド・VPSへの自動デプロイ


## リンク

- [ポートフォリオサイト](https://art-full-stack.com/)
- [GitHub Repositories](https://github.com/TakahiroNago?tab=repositories)
