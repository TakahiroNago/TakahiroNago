# 名合 貴洋｜ソフトウェアエンジニア

C++によるデスクトップアプリケーション・画像処理の開発と、Laravel・Reactを用いたWebアプリケーション開発に取り組んでいます。

実務では、産業機器の制御ソフトウェアや外観検査システムの開発を経験。課題の把握から設計・実装・テストまで、一貫して対応できることが強みです。

個人開発では、C++の画像処理技術とWeb技術の連携に加え、Go・gRPCによるAPI開発、Dockerを用いたサービス構成、AWSへのデプロイ・監視まで取り組んでいます。技術単体だけでなく、各コンポーネントを連携させてアプリケーション全体を構築することを重視しています。

## 技術スタック

- **言語：** C++, C, Go, PHP, JavaScript, TypeScript, Python
- **フレームワーク・ライブラリ：** Laravel, React, OpenCV
- **通信・API：** REST API, gRPC, Protocol Buffers
- **デスクトップ・Web技術：** Tauri, WebAssembly
- **インフラ・開発環境：** AWS (EC2, CloudWatch, SNS), Linux, Docker, Docker Compose, CMake
- **開発ツール：** Git, GitHub, GitHub Actions

## 実務経験

- C/C++による産業機器の制御プログラム開発・機能改修
- C++・画像処理を用いた外観検査システムの開発
- Tauriを用いたデスクトップアプリケーションの開発
- 課題の把握から設計、実装、テストまでの一貫した開発
- Linux・Dockerを用いた開発環境での業務経験

## 個人開発

### [SVG App](https://github.com/TakahiroNago/svg-app) / [Web版デモ](https://svg.art-full-stack.com/) / [AWS版デモ](https://aws-svg.art-full-stack.com/)

C++・OpenCVによるラスター画像からSVGへの変換ツールです。画像処理エンジンをWeb APIと連携させ、ブラウザから利用できるアプリケーションとして構築しています。

- C++・OpenCVによる画像解析、減色、輪郭抽出、SVG生成
- CLIと画像変換コアを分離した設計
- WebAssemblyによるブラウザ上での変換処理
- React・TypeScriptによるWebインターフェース
- GoによるREST APIと、C++によるgRPCサーバーの連携
- Protocol Buffersによるサービス間通信の定義
- Docker Composeによるコンテナ構成
- AWS EC2へのデプロイ、NginxによるHTTPS対応
- GitHub ActionsによるCI/CD
- CloudWatchによるEC2監視と、SNSによるメール通知の設定

**主な技術構成**

`React / TypeScript → Go REST API → gRPC → C++ / OpenCV`

### [PaintMix](https://github.com/TakahiroNago/paint-mix-app) / [Webアプリ](https://paint.art-full-stack.com/)

React・TypeScriptを用いた、絵の具の混色をシミュレーションするWebアプリです。

- ReactによるUIの設計・実装
- TypeScriptによる型を活用した開発
- Mixboxを利用した色の混合処理
- ブラウザ上で利用できるWebアプリケーションの公開
- 日本語・英語の表示対応

### [ZEN App](https://github.com/TakahiroNago/zen-app) / [Webアプリ](https://zen.art-full-stack.com/ja)

Laravel・PHPとOpenAI APIを活用した、禅の考え方を取り入れた対話型Webアプリケーションです。

- LaravelによるWebアプリケーションの設計・実装
- OpenAI APIとの連携によるAI対話機能
- VPSへのデプロイとWebアプリケーションの公開
- アプリケーション設定やプロンプトの管理

## GitHub

各リポジトリに、開発目的・使用技術・実装機能・セットアップ方法などを記載しています。

- [GitHub Repositories](https://github.com/TakahiroNago?tab=repositories)
