# 名合 貴洋｜ソフトウェアエンジニア

**ポートフォリオ：** https://art-full-stack.com/

C/C++による産業機器の制御ソフトウェアや画像処理・外観検査システムの開発と、React・Next.js・Go・Laravelを用いたWebアプリケーション開発に取り組んでいます。

直近の実務では、Tauri（React, Rust）を用いた外観検査装置向けアプリケーションで、制御プログラムとUIの両方を担当し、課題の把握から機能検討・設計・実装・テストまで対応しています。

個人開発では、C++の画像処理技術とWeb技術の連携に加え、Next.js・PostgreSQLによる認証・権限管理を備えたWebアプリケーション開発、Go・gRPCによるAPI開発、Dockerを用いたサービス構成、AWSへのデプロイ・監視まで取り組んでいます。直近では、AIの提案を人間の承認と監査ログのもとで実行するセキュリティ管理プラットフォームを、脅威モデルとセキュリティ設計を文書化しながらLaravel・PostgreSQL・Reactで開発しています。技術単体だけでなく、各コンポーネントを連携させてアプリケーション全体を構築することを重視しています。

## 技術スタック

- **言語：** C, C++, Python, Go, PHP, Rust, TypeScript
- **フロントエンド：** React, Next.js, Vue.js, Vite, WebAssembly, Web Worker, Tailwind CSS, shadcn/ui
- **バックエンド・API：** Go REST API, gRPC, Protocol Buffers, Laravel, Laravel Sanctum, Next.js Server Actions, Better Auth, OpenAI API
- **データベース：** PostgreSQL, Redis, Prisma, MySQL
- **デスクトップ：** Tauri
- **画像処理：** OpenCV
- **テスト：** Pest, Larastan, Vitest, Playwright, axe-core
- **セキュリティ検査：** Semgrep, Trivy, gitleaks
- **インフラ・運用：** Linux（Rocky Linux 9）, Docker / Docker Compose, AWS（EC2, Systems Manager, CloudWatch, SNS）, Nginx, Cloudflare Pages, Vercel, Neon
- **開発ツール：** Git, GitHub, GitHub Actions

## 実務経験

- C/C++による産業機器の制御プログラム開発・機能改修
- C++・画像処理を用いた外観検査システムの開発
- Tauri（Rust, Vue.js, React, TypeScript)を用いたデスクトップアプリケーションの開発
- 課題の把握から設計、実装、テストまでの一貫した開発
- Linux・Dockerを用いた開発環境での業務経験

## 個人開発

### [SecureFlow AI](https://github.com/TakahiroNago/secureflow-ai)

AIが業務内容の依頼文を分析してワークフロー（実行計画）を提案し、入力と出力の検査、人間の承認、実行前の再検証、改ざんを検出できる監査ログを経て実行する、組織向けのセキュリティ管理プラットフォームです。AIにはツール実行・DB・外部通信の権限を与えず、提案のみを行わせる設計にしています。Laravel・PostgreSQL・Redis・Reactで実装し、要件定義・脅威モデル・設計書・テスト戦略を文書化しながら、工程ごとにテスト・静的解析・セキュリティスキャンをCIで通して開発を進め、要件定義で定めた15項目の完成条件を根拠付きで確認してMVPを完成させました。開発環境で動作し、AIは既定でモック、実行は模擬のみです（公開デモはありません。公開環境へ移行する前に満たす条件は設計書に整理しています）。

- 個人情報のマスキング、認証・秘密情報（APIキーなど）による停止、プロンプトインジェクションの検出（High / Critical は停止、Medium は警告、Low は記録）と、検出が完全ではないことの明示
- AIの出力をJSONスキーマ・操作の許可リスト・機密情報・HTMLで検証し、禁止操作の実行ハンドラをコード上に存在させない
- 実行する処理・使用するAI機能・対象データ・必要な権限・実行による影響を人間が確認して承認。承認は計画のSHA-256ハッシュに紐付け、自己承認は禁止、承認後の編集は再承認
- 実行前に承認ハッシュとポリシーを再検証し、Idempotency-Keyで二重実行を防止（実行は模擬のみ）
- 操作を組織ごとのハッシュチェーンで記録する監査ログ（DB関数からのみ追記、更新・削除はトリガーで禁止）と、画面・コマンドからの検証
- 組織・ユーザー・ロールに基づく認可、Sanctumによる同一オリジンのCookieセッション、DBロールの分離（所有者 / アプリ / テスト）
- Pest（セキュリティテストを独立したグループに分離）、Larastan（レベル8）、Vitest、PlaywrightによるE2E（Chromium / Firefox / WebKit）、アプリ内のセキュリティ自己診断（26ケース）
- GitHub Actionsの7つのジョブ（秘密情報スキャン、バックエンド、フロントエンド、全サービス起動、E2E、セキュリティテスト、Semgrep / Trivy）をPull Requestごとに実行し、すべて通過したものだけをmainにマージ
- Redis・PostgreSQL・workerの実際の障害を再現する検証スクリプトと、変異試験によるテストの有効性の確認
- AIコーディングエージェント（Claude Code）を活用し、変更してはならない安全原則を明文化したうえで、各工程の設計判断・承認・レビューを自分で行う進め方

**提案から実行までの経路**

- 分析：`ブラウザ → Nginx → Laravel API（認証・CSRF・認可） → 入力検査（マスキング・秘密情報・インジェクション検出） → worker → AI（提案のみ。既定はモック） → 出力検証（スキーマ・許可リスト・機密情報・HTML除去） → PostgreSQL`
- 承認と実行：`申請者の依頼 → 管理者の承認（SHA-256ハッシュに紐付け。自己承認は不可） → 実行前の再検証（ハッシュ・ポリシー・Idempotency-Key） → 模擬実行 → 監査ログ（ハッシュチェーン）`

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
