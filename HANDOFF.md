# 引き継ぎ書 — 名豊興運版(2026-10-15時点)

新しいセッションで作業を再開する際は、まずこのファイルと [README.md](README.md)・[TECH_DEBT.md](TECH_DEBT.md)・[design/DESIGN.md](design/DESIGN.md) を読んでください。
派生元 A-LOGI版の立ち上げで踏んだ手順と注意点は、A-LOGI版 `hanyama54321-cyber/matomete-alogi` の `HANDOFF.md` に詳しく残っています(このファイルは、そのうち名豊興運版に関係するものを引き継いでいます)。

## このリポジトリについて

- **リポジトリ**: `hanyama54321-cyber/matomete-meiho`(**public**)。名豊興運 専用の「安全配送まとめてアプリ」。
- **派生元**: A-LOGI版 `hanyama54321-cyber/matomete-alogi` の `A-0.1.3`(`main` の `15f483f`)。**履歴は引き継いでいない**(最初の取り込みコミットに出どころを記録)。
  A-0.1.3 は HI-LINE版 `matomete-app` の `v0.4.5` をもとにしている。それまでの経緯・設計判断は matomete-alogi / matomete-app 側の `HANDOFF.md`・`TECH_DEBT.md` を参照。
- **構成**: 単一ファイルSPA([index.html](index.html))+ Firebase(Firestore / Auth / Storage / Cloud Functions / FCM)。機能は A-0.1.3 と同一。
- **公開URL(予定)**: `https://hanyama54321-cyber.github.io/matomete-meiho/`(GitHub Pages、`main` のルート)。**まだ公開していない**
- **配色・アイコン**: [design/DESIGN.md](design/DESIGN.md) を正とする(名豊興運のトラック・社屋の配色。会社ロゴは使わない)。`design/` は消さない
- **版番号**: `M-x.y.z`(HI-LINE版の `v0.x.y`、A-LOGI版の `A-x.y.z` とは別系統)。現在 `M-0.1.0`(未公開)。
- **ブランチ**: 2026-10-15 時点、立ち上げ作業は `claude/gracious-goldberg-qfy7z4` にある。`main` には `design/` の追加コミットだけがある。
  `develop` はまだ作っていない。A-LOGI版と同じ「`main`=公開、`develop`=開発、`develop`→`main` は `--no-ff`、force push しない」運用にするなら、
  南野さんの指示で作業ブランチから `develop` を作る(README の手順)

### A-LOGI版との違い(これ以外は A-0.1.3 と同じ)

| 項目 | A-LOGI版 | 名豊興運版 |
|---|---|---|
| 配信パス | `/matomete-alogi/` | `/matomete-meiho/` |
| Firebase | `matomete-alogi` | `matomete-meiho`(**値は未受領。下の「Firebase の差し替え箇所」**) |
| ブラウザ保存領域のキー | `alogi_fbFcmTokenId` / `alogi_fbMyAnonReportIds` | `meiho_fbFcmTokenId` / `meiho_fbMyAnonReportIds` |
| 名称 | 「安全配送まとめてアプリ A-LOGI」/ 短縮「まとめてA-LOGI」 | 「安全配送まとめてアプリ 名豊興運」/ 短縮「まとめて名豊」 |
| 配色・アイコン | 赤基調・A | 名豊カラー(青基調)・M(下の「配色」) |
| 新着マーク(ベル・タブ) | 黄 `#FFD54F`・濃色リング | レッド `#D6333F`・白リング(HI-LINE版と同じ形) |
| 周知の未読ドット | `--navy`(ダークワイン) | `--navy`(ネイビー `#24366B`) |
| 版番号 | `A-0.1.3` | `M-0.1.0`(更新履歴は M-0.1.0 の1件のみ) |
| 乗務員コードの入力例 | 「例: 40001」 | 「例: 12345」(**名豊興運のコード範囲が決まったら差し替える**) |
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
| 3 | 接続先を `matomete-meiho` に(値は差し替え待ち) | 一部済(`e4d3a45`)。**firebaseConfig と VAPID 鍵は南野さんから受領後** |
| 4 | 配色・アイコン・透かしを名豊カラーに | 済(`df5114e`) |
| 5 | 乗務員・管理者リストの投入準備 | 準備済み(下の「乗務員・管理者リストの投入」)。**実行はしていない** |
| 6 | Firebase プロジェクトの設定・ルールと関数のデプロイ | 未(南野さんのコンソール作業が先) |
| 7 | 初期データ投入 | 未(名簿CSVと `seed.html` の準備が先) |
| 8 | 公開(`main` へのマージ、GitHub Pages の有効化) | 未(南野さんの指示が出てから) |

## Firebase の差し替え箇所(南野さんから値を受け取ったら)

| ファイル | 箇所 | 現在 |
|---|---|---|
| [index.html](index.html) | `firebaseConfig`(先頭の `<script>`) | `projectId: "matomete-meiho"` だけ確定値。ほかは `__MEIHO_API_KEY__` などの仮の文字列 |
| [index.html](index.html) | `FCM_VAPID_KEY` | 空(空のあいだはプッシュ通知の登録をスキップする) |
| [firebase-messaging-sw.js](firebase-messaging-sw.js) | `firebaseConfig` | index.html と同じ仮の値(**index.html と必ず同じ値にする**) |
| [.firebaserc](.firebaserc) | `default` | `matomete-meiho`(済) |
| [test/rules/helpers.js](test/rules/helpers.js) | `PROJECT_ID` | `matomete-meiho`(済。Storage ルールのテストは `.firebaserc` と同じIDでないと失敗する) |
| `seed.html`(リポジトリ外) | `firebaseConfig`・接続先の表示と警告 | 下の「seed.html の用意」 |

- 仮の文字列にしたのは、空文字だと Auth の初期化で例外になり、ログイン画面も出なくなるため。差し替え後は「`__MEIHO_`」で全文検索して残りが無いことを確かめる
- `measurementId` は不要(アプリは Analytics を使っていない)
- `firebaseConfig` と VAPID 公開鍵は公開してよい値(アクセス制御はルールで行う)

### コンソールで必要な設定(A-LOGI版の立ち上げで必要だったもの)

A-LOGI版ではコマンドから作ろうとして Firestore API 未有効で止まり、最終的に南野さんがコンソールで設定した。同じものが `matomete-meiho` にも必要。

- [ ] Blaze プラン(Cloud Functions に必要)と予算アラート(A-LOGI版は $5)
- [ ] Firestore Database(ネイティブモード、ロケーション `asia-northeast1`)
- [ ] Storage(バケット。A-LOGI版は `matomete-alogi.firebasestorage.app` の形だった)
- [ ] Authentication: 「メール/パスワード」を有効、承認済みドメインに `hanyama54321-cyber.github.io`(`localhost` は初期状態で入っている)
- [ ] Cloud Messaging: ウェブプッシュ証明書(VAPID 鍵ペア)を生成 → 公開鍵を `FCM_VAPID_KEY` に
- [ ] ウェブアプリの登録(名前の例:「安全配送まとめてアプリ 名豊興運」)→ `firebaseConfig` を受け取る

**デプロイ時に起きること(A-LOGI版の記録より)**

- Storage ルールは Firestore を参照する(`firestore.get()`)ため、Storage のサービスアカウントに `roles/firebaserules.firestoreServiceAgent` が必要だった(A-LOGI版は南野さんの許可を得て付与)
- Functions のデプロイ(`--dry-run` でも)で API の有効化と Google による IAM の自動付与が起き、初回は Eventarc の権限反映待ちで一部失敗した。数分おいて再デプロイで成功
- Functions のランタイムは `nodejs22`(`firebase.json`。Node.js 20 は 2026-10-30 廃止)
- **IAM・API の設定を失敗の解消のために自分で変えない。** Google がサービスエージェントに自動で付けるロール以外の追加・変更が起きたら止めて報告する(A-LOGI版での取り決め)
- コマンドは必ず `--project matomete-meiho` を付ける。HI-LINE(`anzen-matomete-app`)・A-LOGI(`matomete-alogi`)に対するコマンドは参照も含めて実行しない

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
| 10 | 乗務員の一部に `role: admin` を付け、管理者画面を使わせる | 運用 | 南野さんの指示(2026-10-15)。影響は下の「管理者権限の付与」 |
| 11 | 色分け用の琥珀色 `--amber` | `index.html` | 赤基調で `--primary` と `--danger` が見分けにくかったため。青基調では必須ではないが、色の意味を変えないため残した |
| 12 | メール通知を組み込まない | — | A-LOGI の決定 |

## 乗務員・管理者リストの投入(準備まで。実行はしていない)

### 使う仕組み(A-LOGI版と同じ)

| 何を | 使うもの | 補足 |
|---|---|---|
| 管理者 `AAAAA`・`BBBBB`・`CCCCC` の Auth アカウントと `users` | `seed.html` の ① | 最初の `users/AAAAA` だけはルールの外で作る必要がある(下の手順2) |
| 班2件・チャンネル4件・KYT 7件・手順書サンプル5件 | `seed-teams.js`・`seed-channels.js`・`seed-kyt.js`・`seed-manuals.js`(`seed.html` の ③⑤⑦⑥) | 固定のドキュメントIDで上書きするので2回押しても壊れない |
| 乗務員マスタの CSV 取り込み + Auth アカウントの一括作成 | `seed-drivers-csv.js`(`seed.html` の ⑧。ドライラン → 本実行) | 新規の乗務員は Auth(初期パスワード=乗務員コード)と `users/{コード}`(`role: driver`、`team: null`)が作られる。既存は氏名だけ更新、CSV に無いコードには触らない。`AAAAA`/`BBBBB`/`CCCCC` は常に除外 |
| 管理者権限の付与・初期の所属班 | アプリの「乗務員マスタ」(管理者でログイン)で1人ずつ役割(`driver`/`admin`)と所属班を変える。または、南野さんの了承のうえで Claude Code が所有者の権限で一括変更する(A-LOGI版はこちらで行った) | 乗務員マスタからの「新規登録」は Auth アカウントを作らないので、乗務員の追加は CSV で行う |

`seed-*.js` はこのリポジトリで A-LOGI版と同じもの(乗務員コード5桁・初期パスワード=コード・`AUTH_EMAIL_DOMAIN`・`AUTH_PW_SUFFIX` も同じ)。
`seed-drivers-csv.js` の読み取り処理は、下の形式の架空データで「余分な列は無視される」「`AAAAA` の行は除外対象になる」「引用符付き・4桁は不正行になる」ことを確認した(2026-10-15)。

### seed.html の用意(【要確認】南野さんの作業が必要)

`seed.html` は `.gitignore` で除外していて、**A-LOGI版のリポジトリにも、このリポジトリにも入っていない**(南野さんの PC の作業フォルダ `matomete-alogi` にだけある)。
名豊興運版では、そのコピーを PC の `matomete-meiho` の作業フォルダに置き、次を書き換える(A-LOGI版で HI-LINE版から作ったときと同じ箇所)。

| 箇所 | 変更 |
|---|---|
| `firebaseConfig` | `matomete-meiho` の値に(`index.html` と同じ)。A-LOGI の値(`matomete-alogi`・`252853368767`)が残っていないことを全文検索で確認 |
| 画面上部の接続先の表示と警告 | `matomete-alogi(A-LOGI)` → `matomete-meiho(名豊興運)`。警告の条件も `matomete-meiho` 以外にする |
| ⑧ の説明文 | 名簿の見出しを下の形式に |
| それ以外(① は管理者3件だけ・②④⑨ は削除済み・⑤ は管理者でログインしたら押せる) | A-LOGI版のまま使う |

ファイルを Claude Code に渡してもらえれば書き換えを行う(コミットはしない)。

### 名簿CSVの形式(南野さんに用意してもらうもの)

- **ファイル名**: `名豊興運_乗務員コード一覧.csv`
- **置き場所**: 南野さんの PC の作業フォルダ `matomete-meiho`(`seed.html` と同じ場所)。**リポジトリにはコミットしない**(public のため。`*.csv` は `.gitignore` で除外済み)
- **列**(1行目は見出し。見出しの文字で列を探すので、この文字のまま):

  ```
  乗務員コード,氏名,権限,所属班
  12345,名豊 太郎,乗務員,昼班
  12346,名豊 花子,管理者,夜班
  ```

  - `乗務員コード`・`氏名`: 取り込みに使う列(必須)
  - `権限`(`乗務員` / `管理者`)・`所属班`(`昼班` / `夜班` / 空欄): 取り込み処理は読まない。**管理者権限の付与と初期の所属班を決めるための列**(取り込みのあとで、乗務員マスタまたは一括変更で反映する)
  - `AAAAA`・`BBBBB`・`CCCCC` は入れなくてよい(入れても除外される)
- **チェック項目**(A-LOGI版の投入で確認したもの)
  - [ ] コードはすべて半角英数字5桁。重複なし
  - [ ] **先頭が0のコードがある場合**、Excel で開くと0が消えて4桁になる(不正行になる)。セルの書式を「文字列」にしてから保存する
  - [ ] 引用符(`"`)で囲まれていない(Excel が引用符付きで保存すると全行が不正行になる)
  - [ ] 氏名にカンマ(`,`)が入っていない(そこで切れて登録される。エラーにならない)
  - [ ] 文字コードは UTF-8(Excel なら「CSV UTF-8(コンマ区切り)」)。Shift_JIS だと氏名が文字化けする
  - [ ] 研修用のコードを使うなら CSV に入れる

### 投入の順番(Firebase の設定と `seed.html` の用意が済んでから。A-LOGI版 HANDOFF の「初期データ投入」と同じ)

1. Authentication のサインアップ(「作成を有効にする」)を**オン**にする(`seed.html` は画面からアカウントを作るため)
2. 未ログインで ① → Auth の `AAAAA`・`BBBBB`・`CCCCC` ができる(`users` の作成は拒否されるのが正常)。
   **最初の `users/AAAAA` だけはルールの外で作る**(`name: 管理者A`、`role: admin`、`team: null`、`passwordChanged: false`)。A-LOGI版では南野さんの了承のうえで Claude Code が所有者の権限で1件書き込んだ
3. `AAAAA` / `AAAAA` でログイン → ① をもう一度(`users` 3件)
4. ③ 班 → ⑤ チャンネル → ⑦ KYT → ⑥ 手順書サンプル(任意)
5. ⑧ で名簿CSVを選んで**ドライラン** → 新規の件数・除外0〜3件・不正行0件・氏名の文字化けなしを確かめてから「承認して本実行」
6. `config/notifications` に `openToAllUsers: true`(boolean)を作る
7. 管理者権限の付与・初期の所属班の反映(CSV の `権限`・`所属班` 列から)
8. サインアップを**オフ**に戻す(A-LOGI版では戻し忘れがあったため、読み取りで確認する)
9. 確認: 乗務員マスタの人数 = CSV の乗務員の行数、管理者3件が一覧に出ない、班2・チャンネル4・KYT 7、乗務員コードと初期パスワードでログインできる

### 管理者権限の付与(A-LOGI版で分かった影響)

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
- **`main` へのマージ・タグ付け・Pages の有効化は、南野さんの指示が出てから行う**

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
