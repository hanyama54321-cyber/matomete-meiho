# 引き継ぎ書 — 名豊興運版(2026-10-17時点・M-0.1.0 公開済み)

新しいセッションで作業を再開する際は、まずこのファイルと [README.md](README.md)・[TECH_DEBT.md](TECH_DEBT.md)・[design/DESIGN.md](design/DESIGN.md) を読んでください。
派生元 A-LOGI版の立ち上げで踏んだ手順と注意点は、A-LOGI版 `hanyama54321-cyber/matomete-alogi` の `HANDOFF.md` に詳しく残っています(このファイルは、そのうち名豊興運版に関係するものを引き継いでいます)。

## このリポジトリについて

- **リポジトリ**: `hanyama54321-cyber/matomete-meiho`(**public**)。名豊興運 専用の「安全配送まとめてアプリ」。
- **派生元**: A-LOGI版 `hanyama54321-cyber/matomete-alogi` の `A-0.1.3`(`main` の `15f483f`)。**履歴は引き継いでいない**(最初の取り込みコミットに出どころを記録)。
  A-0.1.3 は HI-LINE版 `matomete-app` の `v0.4.5` をもとにしている。それまでの経緯・設計判断は matomete-alogi / matomete-app 側の `HANDOFF.md`・`TECH_DEBT.md` を参照。
- **構成**: 単一ファイルSPA([index.html](index.html))+ Firebase(Firestore / Auth / Storage / Cloud Functions / FCM)。機能は A-0.1.3 と同一。
- **公開URL**: `https://hanyama54321-cyber.github.io/matomete-meiho/`(GitHub Pages、`main` のルート)。**2026-10-17 に M-0.1.0 を公開済み**(下の「M-0.1.0 の公開」)
- **配色・アイコン**: [design/DESIGN.md](design/DESIGN.md) を正とする(名豊興運のトラック・社屋の配色。会社ロゴは使わない)。`design/` は消さない
- **版番号**: `M-x.y.z`(HI-LINE版の `v0.x.y`、A-LOGI版の `A-x.y.z` とは別系統)。現在 `M-0.1.0`(2026-10-17 公開、タグ `M-0.1.0` = `f4ecb89`)。
- **ブランチ**: A-LOGI版と同じ「`main`=公開、`develop`=開発、`develop`→`main` は `--no-ff`、force push しない」運用(2026-10-17 から)。
  `main` と `develop` はどちらも `f4ecb89`(M-0.1.0 のマージコミット)から始まる。立ち上げに使った `claude/gracious-goldberg-qfy7z4` は役目を終えた(消してよい)。
  **今後の修正は `develop` で行う**

### A-LOGI版との違い(これ以外は A-0.1.3 と同じ)

| 項目 | A-LOGI版 | 名豊興運版 |
|---|---|---|
| 配信パス | `/matomete-alogi/` | `/matomete-meiho/` |
| Firebase | `matomete-alogi` | `matomete-meiho`(プロジェクト番号 `1085038876307`。下の「Firebase プロジェクト」) |
| ブラウザ保存領域のキー | `alogi_fbFcmTokenId` / `alogi_fbMyAnonReportIds` | `meiho_fbFcmTokenId` / `meiho_fbMyAnonReportIds` |
| 名称 | 「安全配送まとめてアプリ A-LOGI」/ 短縮「まとめてA-LOGI」 | 「安全配送まとめてアプリ 名豊興運」/ 短縮「まとめて名豊」 |
| 配色・アイコン | 赤基調・A | 名豊カラー(青基調)・M(下の「配色」) |
| 新着マーク(ベル・タブ) | 黄 `#FFD54F`・濃色リング | レッド `#D6333F`・白リング(HI-LINE版と同じ形) |
| 周知の未読ドット | `--navy`(ダークワイン) | `--navy`(ネイビー `#24366B`) |
| 版番号 | `A-0.1.3` | `M-0.1.0`(更新履歴は M-0.1.0 の1件のみ) |
| 乗務員コード | 40000番台(入力例「例: 40001」) | 30000番台(入力例「例: 30003」)。名簿は `30000`〜`30101` の26名、`30000` は研修用 |
| 背景の透かし | 「A.」 | 「M.」 |
| 名簿CSVの誤コミット防止 | `seed.html` のみ除外 | `seed.html` と `*.csv` を除外 |

**同じもの(A-LOGI版 A-0.1.3 から引き継ぎ)**: ログイン方式(乗務員コード5桁+パスワード、`AUTH_EMAIL_DOMAIN`=`@matomete.local`、`AUTH_PW_SUFFIX`=`_mtm`)、
メンテ用管理者コード `AAAAA`/`BBBBB`/`CCCCC`(乗務員マスタ・チャットのメンバー一覧には出さない)、班(昼班・夜班)、チャンネル(全体連絡・昼班・夜班・管理者)、
ルール(`firestore.rules`・`storage.rules`)、Cloud Functions 8関数、タグラインなし、メール通知なし。

**持ち込んでいないもの**: A-LOGI の乗務員(40000番台)・管理者権限を付けた乗務員・氏名・本番データ・`seed.html`・名簿CSV・A-LOGI の接続情報。

## 進み具合

| ステップ | 内容 | 状態 |
|---|---|---|
| 1 | A-LOGI版 A-0.1.3 のコピーで土台を作る(`design/` は残す) | 済(`5a1d5d6`) |
| 2 | 名称・配信パス・保存キー・版表記の差し替え | 済(`77f806d`) |
| 3 | 接続先を `matomete-meiho` に | 済(`e4d3a45`、値の差し込みは 2026-10-16) |
| 4 | 配色・アイコン・透かしを名豊カラーに | 済(`df5114e`) |
| 5 | 乗務員・管理者リストの投入準備 | 済(2026-10-17)。名簿CSV(26行)と名豊興運用の `seed.html` は PC の作業フォルダにある(リポジトリ外・コミットしない) |
| 6 | Firebase プロジェクトの設定・ルールと関数のデプロイ | 済(2026-10-17、PC の Claude Code と南野さん。下の「デプロイと初期投入の結果」) |
| 7 | 初期データ投入 | 済(2026-10-17。同じく下の「デプロイと初期投入の結果」) |
| 8 | 公開(`main` へのマージ、タグ、GitHub Pages の有効化) | 済(2026-10-17。下の「M-0.1.0 の公開」) |

### 決まったこと(2026-10-16、南野さん)

- **乗務員コードは 30000番台**。名簿は `30000`〜`30101` の26名(`30000` は研修用「名豊興運 研修」)。入力例を「例: 30003」にした
- **初期投入で作る管理者はメンテ用の `AAAAA`・`BBBBB`・`CCCCC` の3件だけ**。乗務員への管理者権限は、運用開始後に南野さんがアプリの「乗務員マスタ」から付ける(初期投入の作業には含めない)。名簿CSVの「権限」列は全員「乗務員」
- **`seed.html`**: 2026-10-16 の連絡では「書き換え済み」だったが、PC を確認したところ**名豊興運用はまだ作られていなかった**(南野さん確認済み)。A-LOGI版のものをコピーして作る(下の「seed.html の作り方」)。リポジトリ外(PC の作業フォルダ)に置き、コミットしない
- **名簿CSV** は用意済み(UTF-8・26行・`parseDriversCsv` で不正行0件を南野さんが確認)。リポジトリには入れない。2026-10-16 に PC の作業フォルダへ `名豊興運_乗務員コード一覧.csv` としてコピーした(下の「名簿CSVの形式」)
- **IAM**: `roles/firebaserules.firestoreServiceAgent` を `service-1085038876307@gcp-sa-firebasestorage.iam.gserviceaccount.com` に付けることを了承(対話モードで聞かれたら Yes)。
  Functions のデプロイで自動で付く権限も了承。取り決めは A-LOGI版と同じ(失敗を直すために権限や API の設定を自分で変えない/一覧に無い権限が増えたら止めて報告/再デプロイは2回まで)。コンテナイメージの保存日数は1日

### 保留中(南野さんの返事待ち)

- 初期の所属班、研修用 `30000` の扱い(当面は全員 `team: null` のまま。乗務員が初回ログイン後に自分で班を選ぶ)
- A-LOGI 由来の設定(下の一覧)を名豊用に変えるか
- 乗務員への管理者権限の付与(運用開始後に南野さんが乗務員マスタから)
- 乗務員向けの案内・マニュアル類(public リポジトリには置かない)

(表示名・ブランチ運用・公開は 2026-10-17 に決定・完了。下の「M-0.1.0 の公開」)

予算アラートは設定済み(2026-10-17、南野さんに確認)。

## M-0.1.0 の公開(2026-10-17、準備室チャットの Claude と南野さん)

公開作業は、当初の予定(Claude Code)ではなく、名豊興運版の「準備室」チャット(claude.ai のクラウドセッション)で行った。その記録。

| 作業 | 担当 | 結果 |
|---|---|---|
| 公開前の点検 | 準備室 | 作業ブランチ `efe44a4` を点検。`main` は祖先(衝突なし)、版表記3か所 `M-0.1.0`、manifest の `start_url`/`scope` と Service Worker の scope が `/matomete-meiho/`、`__MEIHO_…__` の残りなし、名簿・`seed.html`・CSV・鍵の追跡なし |
| 表示名 | 南野さん決定 | 「安全配送まとめてアプリ 名豊興運」/ 短縮「まとめて名豊」のまま確定 |
| アイコン | 南野さん決定 | 現状のまま。`icon-192.png`/`icon-512.png` は四隅が透過のまま `purpose: "any maskable"`(HI-LINE版・A-LOGI版から引き継ぎ)。機種によって角の隙間や端の欠けが出る可能性はあるが、直さないと決定 |
| GitHub Pages の有効化 | 南野さん | Settings → Pages → Deploy from a branch → `main` / `(root)` |
| `main` へのマージ | 準備室 | `claude/gracious-goldberg-qfy7z4` を `--no-ff` でマージ → `f4ecb89`(作業ブランチとの差分0行) |
| `develop` の作成 | 準備室 | `main`(`f4ecb89`)から作成 |
| タグ `M-0.1.0` | 南野さん(PC の Git Bash) | 注釈付きタグ → `f4ecb89`。クラウドセッションからはタグの push が切断されて通らなかった(2回)ため、PC から作成・push。PC の作業フォルダにはリポジトリ単位で `user.name`/`user.email` を設定した |
| 公開URLでの確認 | 南野さん(実機) | 版表記 `Ver.M-0.1.0`・青基調・M アイコン、ホーム画面追加で「まとめて名豊」、乗務員コードでのログイン、「通知設定」の表示 → すべて問題なし |

**分かったこと**
- クラウドセッション(準備室)からは、ブランチの push はできるが**タグの push は通らない**。また `*.github.io` の公開ページにも接続できない(公開後の確認は実機か PC で行う)
- 次回のリリースも README の手順どおり(`develop` → `main` を `--no-ff`、ロールバック用タグ、新版タグ、Pages 反映確認)。タグは PC から付ける

## Firebase プロジェクト `matomete-meiho`

| 項目 | 値 |
|---|---|
| プロジェクトID / 番号 | `matomete-meiho` / `1085038876307` |
| ウェブアプリ | `matomete-meiho-web`(Firebase Hosting なし)、App ID `1:1085038876307:web:47acae409d801c44935f66` |
| 認証ドメイン | `matomete-meiho.firebaseapp.com` |
| Storage バケット | `matomete-meiho.firebasestorage.app`(asia-northeast1) |
| Firestore | `(default)`、asia-northeast1、本番環境モードで作成 |

`measurementId` は入れていない(アプリは Analytics を使っていない)。`firebaseConfig` と VAPID 公開鍵は公開してよい値(アクセス制御はルールで行う)。

### コンソールで済んでいること(2026-10-16、南野さん)

プロジェクト作成・Blaze プラン、Firestore(`(default)`・asia-northeast1・本番環境モード)、Storage(asia-northeast1・本番環境モード)、
Authentication(メール/パスワード有効、承認済みドメインに `hanyama54321-cyber.github.io`)、ウェブアプリ登録、VAPID 鍵の生成。

### 接続情報の差し込み(2026-10-16)

`index.html`・`firebase-messaging-sw.js` の `firebaseConfig`(両方同じ値)と `FCM_VAPID_KEY` に受け取った値を入れた。`.firebaserc`・`test/rules/helpers.js` は `matomete-meiho`。
A-LOGI の値はコードに残っていない(全文検索で確認)。

**確認したこと(読み取りのみ。ログイン・書き込みはしていない)**

| 確認 | 結果 |
|---|---|
| Auth の公開設定(API キーで `getProjectConfig`) | プロジェクト番号 `1085038876307`(`messagingSenderId` と一致)。承認済みドメインに `localhost`・`matomete-meiho.firebaseapp.com`・`matomete-meiho.web.app`・`hanyama54321-cyber.github.io` |
| Storage バケット `matomete-meiho.firebasestorage.app` | 未ログインの一覧取得が 403(バケットはあり、ルールで拒否)。存在しないバケット名では 404 になることも確認 |
| Firebase SDK 10.14.1(アプリと同じ版)で Storage・Firestore を呼ぶ | SDK の既定バケットが `matomete-meiho.firebasestorage.app` になり、読み・書きとも `storage/unauthorized`(ルールの拒否)。Firestore は `permission-denied`。**`.firebasestorage.app` 形式のバケット名で SDK は正しく接続できる**(A-LOGI版も同じ形式で本番稼働している) |
| VAPID 公開鍵 | 65 バイトの P-256 公開鍵(先頭 `0x04`)として正しい形式 |
| ルールテスト | 198件すべて pass(エミュレーターのみ) |

(2026-10-16 時点の記録。ルールは 2026-10-17 にデプロイ済みで、管理者によるファイルのアップロード・削除も実地で確認した。下の「デプロイと初期投入の結果」)

## デプロイと初期投入の結果(2026-10-17、PC の Claude Code)

下の「PC でのデプロイと初期投入の手順」の手順0〜4を行った。コマンドは PC の Claude Code が実行し、対話の質問が出る本実行は南野さんが Git Bash で実行した。
本番の Auth・Firestore・Storage の件数と設定は、ログイン済みの firebase-tools の権限で読み取って確認した(読み取りのみ。書き込みは下の `users/AAAAA` の1件だけ)。

| 手順 | 結果 |
|---|---|
| 0 準備 | firebase-tools 15.23.0、`hanyama54321@gmail.com`、Temurin 21、`.firebaserc` は `matomete-meiho`、名簿CSV 26行(30000〜30101、重複0)。予算アラートは設定済み |
| 1 ルールテスト | 198件すべて pass(エミュレーターのみ) |
| 2 ルール・インデックス | `Deploy complete!`。インデックス2件はリポジトリと一致。**権限の質問には誰も答えていない**(下の「手順書と違ったこと」)が、`roles/firebaserules.firestoreServiceAgent` は付いていた |
| 3 Functions | 初回は8関数のうち6関数が失敗した(Firestore トリガー4件は「Eventarc の権限がまだ反映されていない」、呼び出し型2件は Cloud Build の「予期しないエラー」。A-LOGI版と同じ)。5分後の再実行1回で全件成功。8関数とも `v2`・`asia-northeast1`・`nodejs22`。コンテナイメージの保存日数は1日 |
| IAM | 実行前10件 → 実行後26件。増えた16件はすべて「了承済みの権限」の一覧の中(2段目の3件、3段目の13件)。削除なし。一覧に無い権限は増えていない |
| seed.html | A-LOGI版からコピーして書き換えた(firebaseConfig・接続先の表示と警告・⑤⑧の説明・名前)。A-LOGI の値は0件。A-LOGI用の元のファイルは変わっていない(ハッシュで確認) |
| 4 初期投入 | Auth 29件、`users` 29件(管理者 `AAAAA`/`BBBBB`/`CCCCC` は `role: admin`、乗務員26件は `role: driver`。全員 `team: null`・`passwordChanged: false`。乗務員のコードは CSV の26件と過不足なく一致)。`teams` 2件、`channels` 4件(`general`/`team_a`/`team_b`/`admin`)、`kyt` 7件、`manuals` サンプル5件(⑥ も投入した)、`announcements` 0件、`config/notifications` は `openToAllUsers: true`。サインアップはオフに戻した(`disabledUserSignup: true`) |
| 4 投入後の確認 | 南野さんが `index.html` で確認し、すべて問題なし(版表記、乗務員マスタ26名、班・チャンネル・KYT・手順書、PDF のアップロードと削除、乗務員 `30003` でのログインと「通知設定」の表示)。テストの PDF は削除済みで、Storage は0件 |

- 最初の `users/AAAAA` は案A(PC の Claude Code がログイン済みの firebase-tools の権限で、Firestore の `createDocument` で1件作成。既存なら失敗する方法で、上書きはしていない)で作った
- 控え(すべてリポジトリの外、PC の `../meiho-*`): IAM の JSON(`meiho-iam-before.json`・`meiho-iam-after.json` と途中の段階のもの)、Functions のドライランと初回のログ、ルールテストのログ。氏名は含まない

### 手順書と違ったこと(次回の作業で気をつけること)

- **対話の質問は、アプリの Terminal パネルでは入力が届かなかった。** 手順2の本実行を Claude Code がアプリの Terminal パネルで起動したところ、南野さんが入力した Y が質問に届かなかった。
  同じコマンドを南野さんが Git Bash で実行すると、ルールがすでにアップロード済みとして(`already up to date`)質問が出ないまま公開まで進んだ。
  そのあと、待ったままのタブに Ctrl+C を送ると、firebase-tools は質問だけを閉じ(`[rules] Error checking or updating Cloud Storage for Firebase service account permissions.` と表示)、権限を付けないまま残りのデプロイを最後まで行った(中身は同じルール)。
  **結果として、誰も Y を答えていないのに権限は付いていた**(手順2より前の控えが無いので、いつ付いたかは分からない。コンソールで Storage を作ったときに付いた可能性がある)。
  → 対話の質問が出るコマンドは、最初から南野さんの Git Bash で実行する。質問で待っているプロセスに、止めるつもりで Ctrl+C を送らない
- **seed.html をファイルとして直接開くと、① の Auth 作成が失敗する。** 表示と `projectId` は正しく見えるが、Auth が `file://` からの実行を受け付けない。必ず `http://localhost:8000/seed.html` で開く
- **ログインしたあとの ① の押し直しが抜けやすい。** 今回は抜けていて、`users/BBBBB`・`CCCCC` が作られないまま ③以降が終わっていた。読み取りで気づき、① を押し直して直した
- サインアップをオフにして保存したつもりでも、反映されていないことがあった。保存し直して読み取りで確かめた(A-LOGI版でも戻し忘れがあった)

## PC でのデプロイと初期投入の手順(そのまま使える版)

このクラウドの作業環境には Firebase の認証情報が無い(持たせない)ため、**デプロイと投入は南野さんの PC で行う**(南野さんの手で、または PC の Claude Code で)。
コマンドは Git Bash で、作業フォルダ(リポジトリのルート)から実行する。

**守ること**

- すべての `firebase-tools` コマンドに `--project matomete-meiho` を付ける(`firebase use` の既定値に頼らない)。出力の `Deploying to 'matomete-meiho'...` を見て宛先を確かめる
- HI-LINE(`anzen-matomete-app`)・A-LOGI(`matomete-alogi`)に対するコマンドは参照も含めて実行しない(`projects:list` も使わない)
- **IAM の取り決め(2026-10-16 南野さん決定。A-LOGI版と同じ)**: 失敗を直すために権限や機能(API)の設定を自分で変えない/下の「了承済みの権限」に無い権限が増えたら止めて報告する/再デプロイは2回まで
- サービスアカウントの鍵ファイルは作らない・保存しない。`seed.html`・名簿CSV・IAM の控え(JSON)はコミットしない

**了承済みの権限(2026-10-16)**

| 付く場面 | 権限 ← 付与先 |
|---|---|
| 手順2(Storage ルール)で対話モードの質問に Yes | `roles/firebaserules.firestoreServiceAgent` ← `service-1085038876307@gcp-sa-firebasestorage.iam.gserviceaccount.com` |
| 手順3(Functions)で firebase-tools が質問なしに付ける | `roles/iam.serviceAccountTokenCreator` ← `service-1085038876307@gcp-sa-pubsub.iam.gserviceaccount.com`、`roles/run.invoker`・`roles/eventarc.eventReceiver` ← `1085038876307-compute@developer.gserviceaccount.com` |
| 手順3で API の有効化に伴い Google が自動で付ける | `roles/cloudbuild.builds.builder`(`1085038876307@cloudbuild.gserviceaccount.com`)、各サービスのサービスエージェントへの `roles/cloudbuild.serviceAgent`・`roles/cloudfunctions.standardServiceAgent`・`roles/cloudscheduler.serviceAgent`・`roles/containerregistry.ServiceAgent`・`roles/firebasemods.serviceAgent`・`roles/run.serviceAgent`・`roles/artifactregistry.serviceAgent`・`roles/eventarc.serviceAgent`・`roles/pubsub.serviceAgent`、`roles/editor`(既定の Compute のサービスアカウント・`1085038876307@cloudservices.gserviceaccount.com`・`matomete-meiho@appspot.gserviceaccount.com`) |

(手順3の一覧は A-LOGI版で実際に増えたもの。プロジェクト番号を名豊の `1085038876307` に読み替えている)

### 手順0. 始める前に

- [ ] 【要確認】**予算アラート**が設定されているか(Blaze は従量課金。A-LOGI版は $5)。未設定なら Google Cloud コンソール →「お支払い」→「予算とアラート」で先に作る
- [ ] 作業フォルダを用意する(A-LOGI版の `matomete-alogi` と同じ階層を想定)。`seed.html` と名簿CSVがすでに `matomete-meiho` フォルダにある場合は、いったん別の場所へ移してから clone し、clone のあとで戻す(空でないフォルダには clone できない)
  ```bash
  git clone https://github.com/hanyama54321-cyber/matomete-meiho.git
  cd matomete-meiho
  git checkout claude/gracious-goldberg-qfy7z4
  git log --oneline -1                 # 最新コミットであること
  npm ci
  export PATH="/c/Program Files/Eclipse Adoptium/jre-21.0.11.10-hotspot/bin:$PATH"
  npx firebase-tools --version         # 15.23.0
  npx firebase-tools login:list        # Logged in as hanyama54321@gmail.com
  cat .firebaserc                      # "default": "matomete-meiho"
  ```
- [ ] `seed.html` と `名豊興運_乗務員コード一覧.csv` をこのフォルダに置いたあと、`git status --short` が空であること(どちらも `.gitignore` で除外されている)。
      念のため `git check-ignore -v seed.html 名豊興運_乗務員コード一覧.csv` で2つとも表示されること

### 手順1. ルールテスト(エミュレーターのみ。本番には接続しない)

```bash
npx firebase-tools emulators:exec --only firestore,storage --project matomete-meiho "node --test test/rules/*.test.js"
```

- [ ] 末尾が `# tests 198` / `# pass 198` / `# fail 0`

### 手順2. Firestore ルール・インデックス・Storage ルール

```bash
npx firebase-tools deploy --only firestore:rules,firestore:indexes,storage --project matomete-meiho --dry-run
```

- [ ] `Deploying to 'matomete-meiho'...`、`firestore.rules` と `storage.rules` が `compiled successfully`、最後に `Dry run complete!`
- ドライランでは権限の質問は出ない(firebase-tools 15.23.0 のコードで確認。質問はルールを実際にアップロードするときだけ)

```bash
npx firebase-tools deploy --only firestore:rules,firestore:indexes,storage --project matomete-meiho
```

**`--non-interactive` も `--force` も付けない**(付けると権限の質問が出ず、付与されない)。
**南野さんの Git Bash で実行する**(アプリの Terminal パネルでは質問に入力が届かなかった。2026-10-17)。

- [ ] 途中で `Cloud Storage for Firebase needs an IAM Role to use cross-service rules. Grant the new role? (Y/n)` と聞かれる → **Y**(了承済み)
- [ ] `updated service account for cross-service rules...` と表示され、最後に `Deploy complete!`
- 次の場合は**止めて報告**する(自分で権限を足さない)
  - `[rules] Error checking or updating Cloud Storage for Firebase service account permissions.` という警告が出た
  - 質問が出ないまま終わった(Storage ルールが一度アップロード済みだと「already up to date」で質問ごと飛ばされ、もう一度実行しても出ない。A-LOGI版はこの状態から、同じ処理で権限1件を付けた)
- [ ] コンソールの Firestore →「インデックス」で `reports` の複合インデックス2件が「構築中」→「有効」になる(数分)
- [ ] コンソールの Firestore・Storage の「ルール」タブが、リポジトリの `firestore.rules`・`storage.rules` と同じ内容
- [ ] Google Cloud コンソール →「IAM と管理」→「IAM」で **「Google 提供のロール付与を含める」にチェック**を入れ、
      `service-1085038876307@gcp-sa-firebasestorage.iam.gserviceaccount.com` に「Firebase Rules Firestore Service Agent」が付いている

### 手順3. Cloud Functions(8関数、`asia-northeast1`、`nodejs22`、第2世代)

**(1) 実行前の IAM を控える**(あとで比べるため。控えはリポジトリの外に置く)

- `gcloud` がある場合: `gcloud projects get-iam-policy matomete-meiho --format=json > ../meiho-iam-before.json`
- 無い場合: 上の IAM 画面(「Google 提供のロール付与を含める」にチェック)を画面ごと保存する。A-LOGI版は PC の Claude Code がログイン済みの firebase-tools の権限で読み取った

**(2) ドライラン**

```bash
(cd functions && npm ci)
npx firebase-tools deploy --only functions --project matomete-meiho --dry-run
```

- [ ] `Dry run complete!`
- **ドライランでも API が有効になり、Google の自動付与で権限が増える**(cloudfunctions・cloudbuild・artifactregistry・firebaseextensions・cloudscheduler・run・eventarc など。上の「了承済みの権限」の3段目)

**(3) 本実行**

```bash
npx firebase-tools deploy --only functions --project matomete-meiho
```

- [ ] `How many days do you want to keep container images before they're deleted? (1)` → **1**(了承済み。既定値なので Enter でよい)
- 権限3件(了承済みの2段目)は質問なしに付く
- [ ] 最後に `Deploy complete!`。**一部失敗した場合**(A-LOGI版の初回は、Firestore トリガーが「Eventarc の権限がまだ反映されていない」、ほかが Cloud Build の「予期しないエラー」で失敗した):
      **5分ほど待って同じコマンドをもう一度**。再デプロイは2回まで。成功済みの関数は変更なしで飛ばされる。2回でも失敗したら止めて報告する(権限・API を変えて直そうとしない)

**(4) 確認**

```bash
npx firebase-tools functions:list --project matomete-meiho
```

- [ ] 8行すべて `v2`・`asia-northeast1`・`nodejs22`
  - Firestore トリガー: `onAnnouncementNotify`(written)・`onReportCreated`(created)・`onManualCreated`(created)・`onReportReplyNotify`(updated)
  - 呼び出し型: `sendUnreadReminder`・`subscribeToReport`・`estimateNotifyAudience`
  - 定期実行: `cleanupStaleTokens`(毎週日曜 3:00)
- [ ] 実行後の IAM を(1)と同じ方法で控え(`../meiho-iam-after.json`)、増えたものが「了承済みの権限」の一覧の中だけであること。**一覧に無いものがあれば止めて報告**(元に戻す操作もしない)

### 手順4. 初期データ投入(`seed.html`。名豊興運用を先に作っておく。下の「seed.html の作り方」)

> この手順では本番の Firebase に書き込む。ログインの利用記録(`sessions`)は削除できない。

**(1) 準備**

- [ ] Firebase コンソール → Authentication →「設定」→「ユーザーアクション」→「作成(サインアップ)を有効にする」を**オン**
- [ ] `python -m http.server 8000`(作業フォルダで実行)→ ブラウザで `http://localhost:8000/seed.html`(ファイルを直接開かない。`file://` では ① の Auth 作成が失敗する)
- [ ] 画面上部が「名豊興運」「matomete-meiho」の表示で、警告が出ていない。開発者ツールのコンソールで `firebase.app().options.projectId` が `matomete-meiho`

**(2) 管理者3件(メンテ用 `AAAAA`・`BBBBB`・`CCCCC` のみ。乗務員への管理者権限は初期投入では付けない)**

1. **ログインする前に ①** → ログに「Auth作成」が3件(`users` の作成は拒否されるのが正常。ルール上、管理者しか `users` を作れないため)
2. **最初の `users/AAAAA` だけをルールの外で作る**。どちらで行うかは南野さんが選ぶ
   - 案A: PC の Claude Code が、ログイン済みの firebase-tools の権限で Firestore に1件書き込む(A-LOGI版はこちら)
   - 案B: Firebase コンソール → Firestore →「コレクションを開始」→ コレクションID `users` → ドキュメントID `AAAAA` → フィールド
     `name`(string)`管理者A`、`role`(string)`admin`、`team`(null)、`passwordChanged`(boolean)`false`
3. `seed.html` で `AAAAA` / パスワード `AAAAA` でログイン →「管理者としてログイン中: AAAAA」→ **① をもう一度** → `users` 3件(`AAAAA` は同じ内容で上書き)。
   **③ に進む前に必ず押す**(2026-10-17 は抜けていて、`BBBBB`・`CCCCC` の `users` が無いまま進んでいた)

**(3) 班・チャンネル・KYT・手順書サンプル**(管理者でログインした状態で。2回押しても壊れない)

- [ ] ③ 班 → 2件(昼班・夜班)
- [ ] ⑤ チャンネル → 4件(全体連絡・昼班・夜班・管理者)
- [ ] ⑦ KYT → 7件
- [ ] ⑥ 手順書サンプル → 5件(任意。見た目確認用で実ファイルは無い。不要なら押さない)
- 周知のサンプルは投入しない

**(4) 乗務員(名簿CSV)**

- [ ] ⑧ で `名豊興運_乗務員コード一覧.csv` を選び「ドライラン」
- [ ] **新規26件(`30000`〜`30101`。研修用 `30000` を含む)・更新0件・除外0件(CSV に `AAAAA`〜`CCCCC` の行を入れていれば3件)・不正行0件**。表の氏名が文字化けしていない
      (研修用 `30000` の扱いを決めて CSV から外した場合は新規25件)
- [ ] 一致したら「承認して本実行」。**違っていたら本実行しない**
- 作られるもの: Auth(初期パスワード=乗務員コード)と `users/{コード}`(`role: driver`、`team: null`、`passwordChanged: false`)

**(5) 通知設定を乗務員にも表示する**

- [ ] Firestore →「コレクションを開始」→ コレクションID `config` → ドキュメントID `notifications` → フィールド `openToAllUsers`(boolean)`true`

**(6) 後片付け**

- [ ] Authentication のサインアップを**オフ**に戻し、画面を再読み込みしてオフのままであることを確かめる(A-LOGI版では戻し忘れがあった)
- [ ] `python -m http.server` を止める(Ctrl+C)
- [ ] `git status --short` が空(`seed.html`・CSV がコミット対象に出ていない)

**(7) 投入後の確認**(ローカルの `index.html` からでも本番につながる。`http://localhost:8000/index.html`)

- [ ] `AAAAA` でログインでき、版表記が `Ver.M-0.1.0`
- [ ] 乗務員マスタが26名(`AAAAA`〜`CCCCC` は出ない)。班編成管理に昼班・夜班、チャットのチャンネルが4つ。KYT 7件(手順書サンプルを入れた場合は5件)、周知0件
- [ ] 管理者で手順書に PDF を1つアップロードでき、削除できる(手順2の権限の実地確認)
- [ ] 乗務員コード(例: `30003`)と初期パスワード(=コード)でログインでき、ユーザーメニューに「通知設定」が出る
- [ ] 終わったら Claude Code に連絡(件数・班・チャンネル・設定の読み取り確認を行う)

**初期投入でやらないこと(2026-10-16 決定)**

- 乗務員への管理者権限の付与: 運用開始後に南野さんがアプリの「乗務員マスタ」から行う(下の「管理者権限の付与」に影響の一覧)
- 初期の所属班: 保留中。決まるまでは全員 `team: null` のままで、乗務員が初回ログイン後にプロフィールで自分の班を選ぶ(選ぶまで保存できない・班チャンネルに投稿できない)

### 手順5. 公開(2026-10-17 済み。上の「M-0.1.0 の公開」)

README のリリース手順(`main` へ `--no-ff` でマージ → タグ `M-0.1.0` → GitHub Pages を `main` / root で有効化 → 公開URLで版表記と接続先を確認)。
承認済みドメイン `hanyama54321-cyber.github.io` は設定済み。

## 配色(ステップ4)

[design/DESIGN.md](design/DESIGN.md) の配色トークンを `:root` に当てはめた。CSS のルール数と並びは A-LOGI版 A-0.1.3 と同じ(325、ブラウザの CSSOM で比較して一致)。

| 変数 | A-LOGI版 | 名豊興運版 | 用途・理由 |
|---|---|---|---|
| `--bg` | `#F6F4EE` | `#F4F7FA` | ベース背景 |
| `--surface2` / `--border` | `#FBEFF0` / `#F0DEE0` | `#EBF5FB` / `#DDE6EF` | 淡い面・枠線(青みに) |
| `--primary` | `#C8102E` | `#0B6AA6` | ディープブルー。白文字を載せるボタン・リンク文字(白とのコントラスト比 5.8) |
| `--navy` | `#3A0A12` | `#24366B` | 見出しの文字・濃い面 |
| `--text` / `--text-sub` / `--text-muted` | 赤み | `#1B2645` / `#56637A` / `#687590` | 本文は DESIGN.md の値。補助の2つは白地で 4.5 以上 |
| `--danger` | `#D93A3F` | `#D6333F` | 名豊のレッド(必読・削除・エラー) |
| `--grad` | 赤のグラデーション | `#0A5C92 → #0B6AA6 → #1775B2` | **白文字を載せる面**(ボタン・選択中のチップ・カード・自分の吹き出し・アバター)。どの位置でも白とのコントラスト比 4.9 以上 |
| `--grad-brand`(追加) | — | `#0B6AA6 → #2290CE → #63B8E8` | アイコン地と同じ名豊カラー。**文字を載せない飾り**(ヘッダーの帯・タブの選択線・見出しの縦線)だけ |
| `--badge-color` / `--badge-ring-color` | `#FFD54F` / `#3A0A12` | `#D6333F` / `#FFFFFF` | 新着マーク(ベル・タブ) |
| `--amber` | `#9A5F00` | そのまま | カテゴリ「業務」・KYT難易度「中」・「天気情報」の色分け |

- メインの `#2290CE` を白文字の下地に使わないのは DESIGN.md のルールどおり(白とのコントラスト比 約3.5)。そのため `--grad` は濃い青の範囲にとどめ、`#2290CE`・`#63B8E8` は `--grad-brand` と淡い面(`rgba(34,144,206,…)` など)に使った
- 直書きの色: 管理者のアバター `#0A5C92→#1775B2`、乗務員のアバター `#2290CE`、無効時のログインボタン `#A9B7CE`、オフのスイッチ `#C9D1DD`、
  `theme-color`・manifest の `theme_color` は `#0B6AA6`、`background_color` は `#F4F7FA`
- 派生元からある色(報告の状態色、管理者モードの帯の橙、診断画面の色、`#B36F00` など)は変えていない
- アイコン: `icon.svg`=`design/icon.svg`、`icon-192/512.png`=`design/png/`(角丸・外側透過。manifest の `any maskable` は A-LOGI版と同じ)、
  `icon-180.png`=`design/png/apple-touch-icon-180.png`(角丸なし・全面塗り。iOS が角丸を付ける)、
  ヘッダーのロゴ=`design/icon.svg`、ファビコン(`index.html` に埋め込み)=`design/icon-32.svg`

## 引き継いだ運用設定と、A-LOGI 専用と思われるもの

A-LOGI版 A-0.1.3 の設定をそのまま引き継いでいる。次のものは A-LOGI の事情で決まったもので、名豊興運で変えるかは南野さんの判断待ち。

| # | 設定 | 場所 | A-LOGI での理由 |
|---|---|---|---|
| 1 | 班は「昼班」(`team_a`)・「夜班」(`team_b`)の2つ、班長名を持たない | `index.html` の初期値・`seed-teams.js`・`saveTeamEdit()`・`firestore.rules`(自己変更の許可リスト)・`test/rules/users.test.js` | A-LOGI の勤務体制 |
| 2 | チャンネルは全体連絡・昼班・夜班・管理者(管理者専用)の4つ | `seed-channels.js`・`BADGE_CHANNEL_IDS`・`firestore.rules` | A-0.1.3 で #安全報告 を #管理者 に置き換えた |
| 3 | 班が未設定の乗務員は、プロフィールで班を選ぶまで保存できない | `openProfileEdit()`・`saveProfile()` | 乗務員本人が班を選ぶ運用 |
| 4 | KYT サンプル7件はコンビニ納品の場面 | `seed-kyt.js` | A-LOGI も同じセンター・同じ店舗向けのため |
| 5 | 手順書サンプル5件(任意投入) | `seed-manuals.js` | 見た目確認用 |
| 6 | 周知サンプルは投入しない | `seed-announcements.js` | 季節もので最初の掲示にふさわしくない |
| 7 | 「このアプリについて」の「開発・運用: 名古屋共配センター」「著作権者: 南野」 | `openAppInfo()` | A-LOGI でもそのまま残した |
| 8 | 一般の乗務員にも「通知設定」を出す(`config/notifications` の `openToAllUsers: true`) | Firestore(手作業) | — |
| 9 | 管理者3件・管理者にした乗務員のパスワードは初期値(=コード)のまま運用 | 運用 | 南野さんの判断(2026-10-14・15) |
| 10 | 乗務員の一部に `role: admin` を付け、管理者画面を使わせる | 運用 | 南野さんの指示(2026-10-15)。**名豊興運版では運用開始後に南野さんが画面から付ける(2026-10-16 決定)**。影響は下の「管理者権限の付与」 |
| 11 | 色分け用の琥珀色 `--amber` | `index.html` | 赤基調で `--primary` と `--danger` が見分けにくかったため。青基調では必須ではないが、色の意味を変えないため残した |
| 12 | メール通知を組み込まない | — | A-LOGI の決定 |

## 乗務員・管理者リストの投入(仕組み。実行の手順は上の「手順4」)

### 使う仕組み(A-LOGI版と同じ)

| 何を | 使うもの | 補足 |
|---|---|---|
| 管理者 `AAAAA`・`BBBBB`・`CCCCC` の Auth アカウントと `users` | `seed.html` の ① | 最初の `users/AAAAA` だけはルールの外で作る必要がある(下の手順2) |
| 班2件・チャンネル4件・KYT 7件・手順書サンプル5件 | `seed-teams.js`・`seed-channels.js`・`seed-kyt.js`・`seed-manuals.js`(`seed.html` の ③⑤⑦⑥) | 固定のドキュメントIDで上書きするので2回押しても壊れない |
| 乗務員マスタの CSV 取り込み + Auth アカウントの一括作成 | `seed-drivers-csv.js`(`seed.html` の ⑧。ドライラン → 本実行) | 新規の乗務員は Auth(初期パスワード=乗務員コード)と `users/{コード}`(`role: driver`、`team: null`)が作られる。既存は氏名だけ更新、CSV に無いコードには触らない。`AAAAA`/`BBBBB`/`CCCCC` は常に除外 |
| 管理者権限の付与・所属班の変更(初期投入の後) | アプリの「乗務員マスタ」(管理者でログイン)で1人ずつ役割(`driver`/`admin`)と所属班を変える。**管理者権限は運用開始後に南野さんがこの画面から付ける**(2026-10-16 決定)。A-LOGI版では Claude Code が所有者の権限で一括変更した | 乗務員マスタからの「新規登録」は Auth アカウントを作らないので、乗務員の追加は CSV で行う |

`seed-*.js` はこのリポジトリで A-LOGI版と同じもの(乗務員コード5桁・初期パスワード=コード・`AUTH_EMAIL_DOMAIN`・`AUTH_PW_SUFFIX` も同じ)。
`seed-drivers-csv.js` の読み取り処理は、下の形式の架空データで「余分な列は無視される」「`AAAAA` の行は除外対象になる」「引用符付き・4桁は不正行になる」ことを確認した(2026-10-15)。

### seed.html の作り方(PC で。手順4の前までに)

`seed.html` は `.gitignore` で除外していて、A-LOGI版のリポジトリにも、このリポジトリにも入っていない。
2026-10-17 にこの手順で名豊興運用を作り、PC の作業フォルダ `matomete-meiho` に置いた(コミットしていない)。PC の `matomete-alogi/seed.html` は変わっていない(ハッシュで確認)。
A-LOGI版で HI-LINE版から作ったときと同じやり方で、**コピーしてから書き換える**。

1. コピーする(**`cp`。`mv` にしない**。A-LOGI用の元のファイルには一切書き込まない)
   ```bash
   cp "../matomete-alogi/seed.html" seed.html
   git check-ignore -v seed.html      # .gitignore:3:seed.html と出ること
   ```
2. コピーした `seed.html` だけを書き換える

   | 箇所 | 変更 |
   |---|---|
   | `firebaseConfig` | `index.html` と同じ `matomete-meiho` の値に(`measurementId` は入れない) |
   | 画面上部の接続先の表示と警告 | 「matomete-alogi(A-LOGI)」→「matomete-meiho(名豊興運)」。警告の条件も `matomete-meiho` 以外のときにする |
   | ⑤ の説明 | チャンネル4件=全体連絡・昼班・夜班・**管理者**(A-LOGI版の古い説明で「安全報告」になっていたら直す) |
   | ⑧ の説明 | 名豊の名簿の形(下の「名簿CSVの形式」=見出しなし・B列コード・C列氏名、30000番台)に。管理者の除外はコード(`AAAAA`/`BBBBB`/`CCCCC`)で判定することはそのまま |
   | 画面の名前・タイトルなど | 「A-LOGI」→「名豊興運」 |
   | それ以外(① は管理者3件だけ・②④⑨ は無い・⑤ は管理者でログインしたら押せる・`seed-*.js` の読み込み) | 変えない |

3. 確かめる(数を出すだけ)
   ```bash
   for w in matomete-alogi A-LOGI 252853368767 AIzaSyBnsA1 安全報告 matomete-meiho 1085038876307 名豊興運; do echo -n "$w: "; grep -c "$w" seed.html; done
   grep -c "matomete-meiho" ../matomete-alogi/seed.html   # 0 のまま(A-LOGI用が無事)
   git status --short                                      # 何も出ない
   ```
   - 上の5つ(`matomete-alogi`〜`安全報告`)が **0**、下の3つが **1以上**
4. 開いて表示だけ確認する(ログインもボタン操作もしない): `python -m http.server 8000` → `http://localhost:8000/seed.html`。
   上部が「名豊興運」「matomete-meiho」で警告なし。開発者ツールのコンソールで `firebase.app().options.projectId` が `matomete-meiho`、エラーが出ていない
5. (任意)A-LOGI版と同じく、エミュレーター(`demo-meiho`)で通しの動作確認をしてもよい。本番に書き込まずに①〜⑧を試せる

### 名簿CSVの形式(南野さんが用意済み。2026-10-16 に PC の作業フォルダへ配置)

- **ファイル名**: `名豊興運_乗務員コード一覧.csv`
- **置き場所**: 南野さんの PC の作業フォルダ `matomete-meiho`(`seed.html` と同じ場所)。**リポジトリにはコミットしない**(public のため。`*.csv` は `.gitignore` で除外済み)
- **実際のファイル**(2026-10-16 に PC で確認。氏名は表示せず数だけ見た): 元は `Downloads/乗務員マスタ.csv`。それを `名豊興運_乗務員コード一覧.csv` という名前で作業フォルダにコピーした
  - **見出し行なし**。A列=番号(使わない)・**B列=乗務員コード**・**C列=氏名**(例の形: `3,30000,名豊興運 研修`)。
    `parseDriversCsv()` は見出しが無いとき「B列=コード・C列=氏名」として読む(HI-LINE版からの読み方)ので、このまま使える
  - 26行、B列が30000番台5桁の行 26、コードの重複 0、引用符を含む行 0、UTF-8(BOM付き。BOM は読み取り時に外れる)
  - `権限`・`所属班` の列は無い(権限は全員乗務員として投入し、管理者権限は運用開始後に画面から付けるため不要。所属班は保留中)
  - `AAAAA`・`BBBBB`・`CCCCC` の行は無い(入っていても除外される)
  - 同じ `Downloads` にある `乗務員マスタ (7).csv`・`乗務員マスタ - 乗務員マスタ (4).csv` は **HI-LINE の名簿なので使わない**
- **(参考)見出し付きで作る場合の形**: 1行目を `乗務員コード,氏名` にすれば、見出しの文字で列を探す(余分な列は無視される)
- **チェック項目**(A-LOGI版の投入で確認したもの)
  - [ ] コードはすべて半角英数字5桁。重複なし
  - [ ] **先頭が0のコードがある場合**、Excel で開くと0が消えて4桁になる(不正行になる)。セルの書式を「文字列」にしてから保存する
  - [ ] 引用符(`"`)で囲まれていない(Excel が引用符付きで保存すると全行が不正行になる)
  - [ ] 氏名にカンマ(`,`)が入っていない(そこで切れて登録される。エラーにならない)
  - [ ] 文字コードは UTF-8(Excel なら「CSV UTF-8(コンマ区切り)」)。Shift_JIS だと氏名が文字化けする
  - [ ] 研修用 `30000` を入れるかは保留中(現在の CSV には入っている)

### 投入の順番

上の「PC でのデプロイと初期投入の手順」の**手順4**にまとめた(ルール・Functions のデプロイが先)。

### 管理者権限の付与(運用開始後に南野さんが画面から。A-LOGI版で分かった影響)

`role: admin` にした乗務員は管理者の画面だけになり、乗務員としての機能(必読の確認・KYT・報告の投稿)は使えない。匿名を含む全報告が見える。
既読率・到達率・KYT 進捗の母数から外れる。必読・手順書追加・未読リマインダーの通知は届かず、新着報告の通知が届く。ほかの人の権限を変えられる(自分の権限は変えられない)。
チャットの #管理者 のメンバーになる(`AAAAA`/`BBBBB`/`CCCCC` はメンバー一覧に出ない)。

## 守ること

- **`matomete-app`(HI-LINE版)・`matomete-alogi`(A-LOGI版)は読むだけ。一切変更しない**(ブランチ・タグ・Issue も含む。データにも影響を与えない)
- **機能の追加・削除・挙動の変更をしない**(A-0.1.3 と同じ動きを保つ)
- **次の箇所には手を入れない**
  - `.chip-row` 本体(3か所で共有。折り返しが必要な箇所は派生クラス `.chip-row.wrap` を利用側に付ける)
  - `BADGE_EPOCH`(新しいインスタンスはデータが空なので現行の値のままで影響はない)
  - `AUTH_EMAIL_DOMAIN` / `AUTH_PW_SUFFIX`(`seed.html`・`seed-drivers-csv.js` と一致している必要がある)
  - `localStorage` のキーの `meiho_` 接頭辞(HI-LINE版・A-LOGI版と同じドメインで保存領域を共有するため、外すと互いに上書きする)
- **メール通知は実装しない**
- **想定と違うもの・判断に迷うものが出たら、自分で決めずに止めて報告する**
- **`main` へのマージ・タグ付け・Pages の設定変更は、南野さんの指示が出てから行う**(M-0.1.0 は 2026-10-17 公開済み)

### 公開してはいけないもの

このリポジトリは **public** で、GitHub Pages は `main` のルートをそのまま配信する(`design/` などの下位フォルダも URL で取得できる)。次のものはコミットしないこと。

- 乗務員名簿(CSV)、氏名の一覧
- パスワード、`serviceAccountKey.json` などの鍵ファイル
- 管理者マニュアル・ドライバー用ガイド・早見表などの配布物(管理者コードや「初回パスワードは乗務員コードと同じ」といった運用が書かれているため)
- `seed.html`(管理者専用の投入ツール。`.gitignore` で除外済み)

## 設計上の原則(HI-LINE版から引き継ぎ。改修時に必ず守ること)

- **タブごとに、通知センターとタブの新着マークが同じ判定関数を見る。** 通知センター専用の既読フラグやクエリは作らない
- **ベルの点灯 = 通知センターに出る項目が1件以上。** チャットの新着ではベルは点灯しない(チャットタブのドットのみ)
- **onSnapshotミラー配列**: ログイン時に `attachXxxListener()` を開始し、ログアウト時(`showLoginScreen()`)に必ず unsubscribe
- **管理者の one-shot 集計は必ず `st.role === 'manager'` でガードする**(`users` の一覧取得はルール上 admin 限定)
- **閲覧と書き込みの権限を分ける場合は判定を別々に保つ**
- **本人による単一フィールドの自己更新**は `affectedKeys().hasOnly([...])` で行い、その値を別のルールが信頼する場合は値の許可リストも必須
- **冪等シードスクリプト**: 固定ドキュメントIDで `.set()`。`seedXxx(db, log)` の形
- **利用者の入力を画面に埋め込むときは、必ず `escHtml()` を通す**
- 新しいグローバル関数・定数を定義する前に、**必ず全文検索で同名の有無を確認する**(後勝ちで静かに上書きされる)
- 共有CSSクラスを変更する前に、**必ず全使用箇所を確認する**。CSS の構造を変えたら、ブラウザの CSSOM で**ルール総数と並び**を確認する
- クリックハンドラに文字列を埋め込まない(`bindDataClick()` を使う)

## テスト

```bash
npm ci
npx firebase-tools emulators:exec --only firestore,storage --project matomete-meiho "node --test test/rules/*.test.js"
```

`test/rules/` に12ファイル・**198件**。2026-10-15 にクラウドの作業環境(Linux)で全件 pass(エミュレーターのみ。本番には接続しない)。

- エミュレーターには Java が必要(A-LOGI版の PC では Temurin 21 JRE に PATH を通していた)
- **クラウドの作業環境では、プロキシの環境変数(`HTTPS_PROXY` など)を外して実行すること。** 付けたままだと Storage ルールから Firestore への参照が失敗し、
  「adminはmanualsファイルをアップロードできる」「同・削除できる」の2件が失敗する(A-LOGI版の元のファイルでも同じ結果になることを確認済み。コードの問題ではない)
  ```bash
  env -u HTTP_PROXY -u HTTPS_PROXY -u http_proxy -u https_proxy npx firebase-tools emulators:exec ...
  ```

### 画面の撮影方法(エミュレーター)

本番につながずに画面を確認するため、**リポジトリのファイルは書き換えず**、作業用フォルダにコピーした `index.html` の `firebaseConfig` を `demo-meiho`
(`demo-` で始まるIDは実在のプロジェクトに接続しない)にし、`useEmulator()` を差し込んで、ローカルサーバー経由でブラウザ自動操作で撮影した(2026-10-15)。
仮データ(管理者1名・昼班/夜班の乗務員・周知3件)はエミュレーターにだけ入れた。撮影用のスクリプトはリポジトリに入れていない。

## コミット時の運用ルール

- コミットは作業のまとまりごとに分ける
- コミット前に `git status` で意図しない差分がないか確認する。`.claude/`・`seed.html`・名簿CSV はコミットしない
- リリースを確定と言われたら、実機確認の結果報告があるまで開発ブランチに変更を積まない

## 既知の技術的負債

[TECH_DEBT.md](TECH_DEBT.md) を参照(HI-LINE版 v0.4.5・A-LOGI版 A-0.1.3 時点の記録をそのまま引き継いでいる)。名豊興運版でも当てはまる主なもの:

- **ゲームタブ**は「近日公開」のプレースホルダーのみ
- **乗務員マスタからの個別登録は Auth アカウントを作らない**(項目2b)。ログインできるアカウントの作成は `seed.html` の CSV 投入で行う
- **周知の予約配信は自動公開されない**(項目4。管理者の「今すぐ配信」のみ)
