# 名合 貴洋｜ソフトウェアエンジニア

**ポートフォリオ：** https://art-full-stack.com/

C/C++による産業機器の制御ソフトウェアや画像処理・外観検査システムの開発と、React・Next.js・Go・Laravelを用いたWebアプリケーション開発に取り組んでいます。

直近の実務では、Tauri（React, Rust）を用いた外観検査装置向けアプリケーションで、制御プログラムとUIの両方を担当し、課題の把握から機能検討・設計・実装・テストまで対応しています。

個人開発では、C++の画像処理技術とWeb技術の連携に加え、Next.js・PostgreSQLによる認証・権限管理を備えたWebアプリケーション開発、Go・gRPCによるAPI開発、Dockerを用いたサービス構成、AWSへのデプロイ・監視まで取り組んでいます。技術単体だけでなく、各コンポーネントを連携させてアプリケーション全体を構築することを重視しています。

## 技術スタック

- **言語：** C, C++, Python, Go, PHP, Rust, TypeScript
- **フロントエンド：** React, Next.js, Vue.js, Vite, WebAssembly, Web Worker, Tailwind CSS, shadcn/ui
- **バックエンド・API：** Go REST API, gRPC, Protocol Buffers, Laravel, Next.js Server Actions, Better Auth, OpenAI API
- **データベース：** PostgreSQL, Prisma, MySQL
- **デスクトップ：** Tauri
- **画像処理：** OpenCV
- **テスト：** Vitest, Playwright, axe-core
- **インフラ・運用：** Linux（Rocky Linux 9）, Docker / Docker Compose, AWS（EC2, Systems Manager, CloudWatch, SNS）, Nginx, Cloudflare Pages, Vercel, Neon
- **開発ツール：** Git, GitHub, GitHub Actions

## 実務経験

- C/C++による産業機器の制御プログラム開発・機能改修
- C++・画像処理を用いた外観検査システムの開発
- Tauri（Rust, Vue.js, React, TypeScript)を用いたデスクトップアプリケーションの開発
- 課題の把握から設計、実装、テストまでの一貫した開発
- Linux・Dockerを用いた開発環境での業務経験

## 個人開発

### [ProjectFlow](https://github.com/TakahiroNago/project-management-app) / [デモ（登録せずに試せます）](https://projectflow.art-full-stack.com/login)

個人開発者・小規模チーム（2〜10人）向けのプロジェクト管理Webアプリケーションです。プロジェクト単位でタスクを管理し、進捗・優先度・期限を把握できます。Next.js（App Router）とPostgreSQLで実装して本番公開しており、認証・権限管理・ユーザー間のデータ分離に加え、単体・統合・E2Eテスト、承認付きのデプロイ、本番DBの自動バックアップまで整えています。

- カンバンボード（未着手 / 進行中 / 完了）のドラッグ＆ドロップによる列の移動・並べ替え（マウス・タッチ・キーボード対応）
- プロジェクトの検索・絞り込み・並べ替えと進捗率表示、ダッシュボード、タスクの期限切れ・期限間近の表示
- メンバー管理、タスクへのコメントと更新履歴、ダークモード・レスポンシブ対応
- Better Authによるメール＋パスワード認証、メールでのパスワード再設定、登録不要のデモ（サンプルデータ入りの一時アカウントを1〜2日後に自動削除）
- Owner / Memberの権限管理とユーザー間のデータ分離（所属外のプロジェクトは404として扱う）、nonce付きCSP、認証APIのレート制限
- 権限表・進捗率・日付判定などのビジネスロジックを純粋関数として分離
- PostgreSQL・Prismaによるトランザクション処理と、「各プロジェクトのOwnerはちょうど1人」のDBトリガーによる保証
- Vitest（単体・統合）、Playwright（E2E）、axe-core（全主要画面でのWCAG 2.1 AAの自動チェック）によるテストと、GitHub ActionsによるCI
- Vercel・Neon・Resendでの本番運用と、手動実行・承認付きのGitHub Actionsワークフローによるマイグレーション・デプロイ
- GitHub Actionsによる本番DBの毎日のバックアップ（`pg_dump`、空のDBへの復元による検証、GnuPGでの暗号化、Cloudflare R2での保管）

**リクエストの経路**

- 入口：`ブラウザ → proxy.ts（Cookieが無ければ/loginへ誘導するだけ）`
- 読み取り：`ブラウザ → Server Components → requireUser()（DBでセッション検証） → queries.ts → Prisma → PostgreSQL`
- 更新：`ブラウザ → Server Actions → 認証 → Zod検証 → service.ts（認可＋トランザクション） → Prisma`
- 認証：`ブラウザ → /api/auth/*（Better Auth）`

### [SVG App](https://github.com/TakahiroNago/svg-app) / [Webフロントエンド](https://github.com/TakahiroNago/svg-web) / [デモ（ブラウザ内変換）](https://svg.art-full-stack.com/) / [AWS版（サーバー側変換）](https://aws-svg.art-full-stack.com/)

ラスター画像をSVGに変換するWebアプリケーションです。C++20とOpenCVで実装した変換エンジンを、ブラウザ内のWebAssemblyと、Go REST APIからgRPC経由で呼び出すサーバー側の、2つの経路から利用できる構成にしています。

- C++20・OpenCVによる減色（Lab色空間でのk-means）、輪郭抽出、SVG生成
- 変換コアをCLIから分離し、WebAssemblyとgRPCサーバーで共通利用
- React・TypeScriptによるWebインターフェースと、ブラウザ内変換でのWeb Workerによる処理
- 400万画素を超える画像の自動縮小と、サーバー送信前のメタデータ除去
- Go REST APIとC++ gRPCサーバーの連携、Protocol Buffersによるサービス定義
- AWS EC2上でのDocker Composeによるサービス管理と、NginxによるHTTPS終端
- Cloudflare Pagesでのブラウザ内変換版の公開
- GitHub ActionsによるCI（バックエンド：proto・Go・C++・統合テスト、フロントエンド：lint・型チェック・Vitest・本番ビルド）と、AWS Systems Manager経由の自動デプロイ
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
