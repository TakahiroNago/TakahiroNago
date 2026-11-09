# 名合 貴洋｜ソフトウェアエンジニア

**ポートフォリオ：** https://art-full-stack.com/

実務では、C/C++による船舶制御システムの改修と操船システムの新規開発（リーダー）を経て、Tauri（Rust）によるロボットアーム制御パッケージと外観検査装置ソフトウェアを、プログラム担当1名として設計から実装まで担当しました（2023年10月〜2026年8月）。外観検査の画像処理では、既存のC++実装で約14秒かかっていた処理をRustで約3秒に短縮しています。

個人開発では、AIの提案を人間の承認と監査ログのもとで実行するセキュリティ管理プラットフォーム（SecureFlow AI）をはじめ、Next.js・PostgreSQLによる認証・権限管理を備えたWebアプリケーション、Go・gRPCによるAPI、C++画像処理エンジンのWebAssembly / gRPCからの利用、AWSへのデプロイ・監視まで取り組んでいます。Rustのライブラリ（egui、wry）には修正PRを提出し、LLMアプリケーション向けの入出力検査ライブラリ（llm-inspect）をRustで開発中です。

関心領域：AI機能を安全に組み込むシステム開発、AI機能のセキュリティ、Rustによる開発とOSSへの参加。

## 実務経験（2023年10月〜2026年8月）

実務と個人開発は分けて記載しています。各案件の規模・役割・技術は[ポートフォリオサイトの経歴](https://art-full-stack.com/#experience)に記載しています。

**マイクロクラフト株式会社（2025年5月〜2026年8月）** — プログラム担当1名として設計〜実装を単独で担当

- 外観検査装置の画像認識プログラムとUIの作成：プリント基板のパターン印刷を印刷前後で比較して欠陥を検出。画像処理を約14秒から約3秒へ短縮（並列化、撮影途中からの部分処理、メモリ共有によるI/O削減）— Tauri（Rust, TypeScript, React）、C/C++、HALCON
- ロボットアーム制御パッケージの作成：基板を搬入カートから基板検査機へロード／アンロードし、検査結果に基づいて移動。基板検査機との連携も設計・開発 — Tauri（Rust, TypeScript, Vue.js）、C/C++

**株式会社エスユーエス（2023年10月〜2025年4月）** — 船舶制御装置メーカーに常駐

- 操船システムの新規開発（2024年3月〜2025年4月、リーダー）：要件定義・設計・開発に加え、進捗管理、GitLabの組織内への新規導入とコードレビュー・マージ。Rocky Linux 9とDockerで制御（C++）とUI（Python）を別コンテナで構成 — C/C++、Python、Docker、Rocky Linux、Ubuntu、GitLab
- 操艦システム、自動船位保持システム（DPS）、自動操船装置の改修・調整・実装（メンバー）— C/C++、Cygwin、iTron OS
- 船舶ディーゼルエンジン性能測定システムの改修・新機能追加（メンバー）— C++、C++ Builder
- 船体姿勢シミュレーターのC++からVB.NETへのリプレイス・機能追加（メンバー）— VB.NET

## OSS活動（2026年11月。いずれも提出済み・レビュー中）

- [emilk/egui #8849](https://github.com/emilk/egui/pull/8849)：システムフォントから全角英数字・CJK約物が欠落する問題の修正（PR）
- [tauri-apps/wry #1924](https://github.com/tauri-apps/wry/pull/1924)：Windowsで `WM_SETFOCUS` 時のWebViewへのフォーカス移動を遅延させる修正（PR）
- [MicrosoftEdge/WebView2Feedback #5799](https://github.com/MicrosoftEdge/WebView2Feedback/issues/5799)：同一プロセス内の2つのWebView2ウィンドウを切り替えるとIMEの変換候補UIが画面左上へ外れる不具合の報告（Issue）

## 技術スタック

「自力で設計・実装できる」「実務で使用した」「個人開発・学習で使用した」の3つに分けています。1つの技術が複数に入ることがあります。

- **自力で設計・実装できる：** C, C++, Rust, Tauri, TypeScript, React, Vue.js, Next.js, Python, Go, PHP / Laravel, VB.NET, HALCON, OpenCV, PostgreSQL, MySQL, Docker / Docker Compose, Linux（Rocky Linux 9, Ubuntu）, AWS, WebAssembly, gRPC / Protocol Buffers, Git / GitHub Actions / GitLab
- **実務で使用した：** C, C++, Rust, Tauri, TypeScript, React, Vue.js, Python, VB.NET, C++ Builder, HALCON, OpenCV, Docker / Docker Compose, Linux（Rocky Linux 9, Ubuntu）, iTron OS, Cygwin, Git / GitLab, Windows
- **個人開発・学習で使用した：** Rust, C++20, TypeScript, React, Next.js, Python, Go, PHP / Laravel, Laravel Sanctum, Better Auth, OpenAI API, PostgreSQL, MySQL, Redis, Prisma, OpenCV, WebAssembly, Web Worker, gRPC / Protocol Buffers, Tailwind CSS, shadcn/ui, Pest, Larastan, Vitest, Playwright, axe-core, Semgrep, Trivy, gitleaks, Docker / Docker Compose, AWS（EC2, Systems Manager, CloudWatch, SNS）, Nginx, Cloudflare Pages, Vercel, Neon, GitHub Actions

## 個人開発（2026年9月〜）

開発にはAIコーディングエージェント（Claude Code）を活用し、要件定義・設計判断・レビュー・承認は自分で行っています。

### [llm-inspect](https://github.com/TakahiroNago/llm-inspect)（Rust、2026年11月〜開発中）

LLMアプリケーションの入力（個人情報・秘密情報・プロンプトインジェクション）と出力（JSON Schema・許可リスト・HTML・サイズ）を検査するライブラリとCLIです。全角文字やゼロ幅文字による回避を防ぐため、NFKC正規化と不可視文字の除去を行ったうえで照合し、検出位置は元のテキストのバイト位置へ対応付けて返します。ルールはTOMLで定義する正規表現（日本語・英語）で、Luhn検証、深刻度に応じた許可／警告／遮断の判定、マスキングに対応しています。検査結果には一致した本文を含めない設計です。

- clippy（pedantic）警告ゼロ、テスト44件。GitHub ActionsでUbuntu / Windowsのテスト、wasm32ビルド、MSRV（Rust 1.85）を検証
- 検出は完全ではないことをREADMEに明記。crates.ioは未公開。MIT / Apache-2.0

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
- 変更してはならない安全原則を明文化したうえで、AIコーディングエージェントを活用して開発

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

### [soul_search](https://github.com/kredo-school/soul_search)（2023年4月〜5月）

プログラミングスクールKredoでチーム開発したLaravel製のSNSアプリケーションです（英語での受講・開発。公開デモはありません）。

## リンク

- [ポートフォリオサイト](https://art-full-stack.com/)
- [GitHub Repositories](https://github.com/TakahiroNago?tab=repositories)
