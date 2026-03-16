# Kamukafu Obsidian — Think to Text Protocol のための Vault テンプレート

> **テキストで考えよ。成果物は AI と共につくる。**

## かむかふ（kamukafu）とは

「かむかふ」（かむがふ）は、「考える（かんがえる）」の古形。

国語学の通説では「**か**（処・方向）＋ **むかふ**（向かう・対う）」と分解し、原義は「二つの事柄を向き合わせて比較・検討すること」とされる。

一方、この Vault テンプレートの名前には、もう一つの解釈を込めている：

- **む** — 身（からだ）
- **かふ** — 交う（まじわる）

すなわち「考える」とは「身をもって交わること」。思考は抽象的な脳内活動ではなく、身体的な行為だという読み。この Vault は、その身体性を「書くこと」に見出す。キーボードを叩き、言葉を紡ぐことが、思考そのものになる。

## Think to Text Protocol

AI 時代において、人間の仕事はどう変わるか。

これまで我々は Excel、PowerPoint、Figma といったツールに直接書いてきた。思考と成果物の作成を同時にやるのが最も効率的だったからだ。しかし AI の登場により、この前提に歪みが生じている。

人間がツールに直接書いたデータには「思考」という栄養が入っている。しかしその栄養は、ツール固有のフォーマット（セルの配置、スライドのレイアウト、ボードの座標）に閉じ込められている。他のフォーマットに変換しにくく、AI にも読み取りにくい。

**Think to Text Protocol** は、この分離を提案する：

- **人間の仕事：Think → Text**（思考をプレーンテキストに落とす）
- **AI+人間 の仕事：Text → Output**（テキストを成果物に変換する）

Protocol（プロトコル）とは、異なる主体の間で確実にやり取りするための取り決め。HTTP がブラウザとサーバーの間の約束であるように、Think to Text Protocol は人間と AI の間の約束だ。

テキスト（言語）は、人間と AI が共有できるユニバーサルな中間表現である。コンパイラ設計における中間表現（IR）のように、同じテキストから PowerPoint、Notion ページ、Figma のワイヤーフレーム、メール文面を並列生成できる。ツールに直接書いていたら、この多対多変換は不可能だった。

## 設計思想

### Evergreen Notes

この Vault は Andy Matuschak の [Evergreen Notes](https://notes.andymatuschak.org/Evergreen_notes) の思想に基づいている。

- **ノートはアトミックであるべき** — 1つのノートに1つの概念
- **ノートは概念指向であるべき** — 本・著者・プロジェクト単位ではなく、概念単位で書く
- **ノートは密にリンクされるべき** — `[[wikilinks]]` で思考を接続する
- **階層より連想を優先する** — トップダウンの分類より、ノート間のリンクで構造を作る
- **ノートはまず自分のために書く** — 出版ではなく、自分の思考のために

Evergreen Notes は書き捨てではなく、時間とともに育てるノート。Inbox に走り書きし（Fleeting Notes として）、自分の言葉で咀嚼したら Notes に昇格させる。

### kepano の File over app 哲学

Obsidian の CEO である Steph Ango（kepano）の [File over app](https://stephango.com/file-over-app) 哲学：

> *File over app is a philosophy: if you want to create digital artifacts that last, they must be files you can control, in formats that are easy to retrieve and read. Use tools that give you this freedom.*

- アプリは消える。ファイルは残る
- プレーンテキストは最も長寿なフォーマット。Markdown はその上に構築された軽量な構造化記法
- データの所有権はユーザーにあるべき

この Vault は Markdown ファイルの集合体であり、Obsidian がなくても任意のテキストエディタで読み書きできる。AI にとっても、プレーンテキストは最も扱いやすいインターフェースとなる。

### 著者の追跡（author / editor）

すべてのノートに `author` プロパティを付与し、思考の主体を明示する。AI と人間の協働が当たり前になった時代に、「誰が考えたか」を記録することは重要になる。

| パターン | 意味 |
|---|---|
| `author: yourname` | あなたが書いた |
| `author: yourname` + `editor: claude` | あなたの思考を AI が清書した |
| `author: claude` | AI が生成した |
| `author: claude` + `editor: yourname` | AI が生成し、あなたが監修した |

## Vault 構造

```
.
├── Inbox/          — 未整理の走り書き（Fleeting Notes）
├── Notes/          — 自分の言葉で咀嚼した思考（Evergreen Notes）
├── Daily/          — 日誌（YYYY-MM-DD.md）
├── Projects/       — 案件・プロジェクトの作業足場
├── References/     — 人物・書籍・概念の参照カード
├── Clippings/      — Web クリッパーで保存した記事
├── Emails/         — メールのアーカイブ
├── Generated/      — AI が生成・維持するコンテンツ
│   ├── Context/    — AI が維持する思考設計図
│   ├── Knowledge/  — AI が構築したナレッジ
│   ├── Sessions/   — AI との対話セッション記録
│   └── Logs/       — ツール操作ログ
└── Libraries/      — Vault のインフラ
    ├── Templates/  — Templater テンプレート
    ├── Bases/      — Bases ビュー定義（.base）
    ├── Categories/ — カテゴリインデックス
    └── Binaries/   — 添付ファイル（画像等）
```

### 各フォルダの位置づけ

#### Inbox/ — 思考の入り口

Zettelkasten でいう Fleeting Notes。頭に浮かんだこと、気になったこと、誰かに言われたことを、整理せずにそのまま放り込む場所。ここに書くことにルールはない。走り書きでいい。大事なのは「頭の外に出す」こと。

Inbox にあるノートは未消化の素材であり、あなたの思考ではまだない。

#### Notes/ — あなたの思考の本体

Vault の核心。Evergreen Notes の思想に基づき、出典や他人の言葉への依存を外して、自分の言葉で咀嚼した思考を書く場所。新規ファイルのデフォルト保存先でもある。

1つのノートに1つの概念（アトミック）。`[[wikilinks]]` で他のノートと密にリンクする。書き捨てではなく、時間とともに育てる。この Vault で最も重要なフォルダ。

Think to Text Protocol の「Text」はここに蓄積される。

#### Daily/ — 日々のアンカー

日誌。`YYYY-MM-DD.md` 形式でその日の出来事・思考・タスクを記録する。テンプレートから自動生成される。

Daily は思考の時系列インデックスとして機能する。「あの話はいつ考えたか」を辿る起点になる。Notes が概念軸なら、Daily は時間軸。

#### Projects/ — 実行の足場

案件ごとにサブフォルダを切り、業務一次資料を置く作業場。各プロジェクトの核は `Product.md`（最新仕様書）。タスクリスト、調査メモ、成果物ドラフトもここに置く。

Notes との違いは明確で、Notes はあなたの思考（概念・原則・洞察）、Projects は特定の案件に紐づく実務資料。「疎結合設計とは何か」は Notes に、「A社のシステムを疎結合で設計する」は Projects に書く。

AI との協働が最も活発になるフォルダでもある。

新規案件を始めるときは `Projects/_Template/` をフォルダごとコピーしてリネームする：

```bash
cp -r Projects/_Template Projects/MyNewProject
```

テンプレートの中身：

| ファイル | 役割 |
|---|---|
| `Product.md` | 最新仕様書。プロジェクトの真実の源泉（Single Source of Truth）。仕様・決定事項・予算・体制を記録する |
| `Project.md` | プロジェクト概要・ゴール・タスク管理。何をやるか、なぜやるか、どこまで終わったか |

必要に応じて調査メモや成果物ドラフトを同じフォルダに追加していく。

#### References/ — 人物・概念の参照カード

人、書籍、組織、技術用語など、繰り返し参照する対象のカード。Notes が「あなたが考えたこと」なら、References は「あなたが参照するもの」。

`[[本居宣長]]` や `[[AndyMatuschak]]` のように、Notes から wikilink で参照される。

#### Clippings/ — 外部からのインプット

Web クリッパーで保存した記事や URL。まだ咀嚼されていない外部情報の素材置き場。

Clippings はあなたの思考ではない。読んで咀嚼し、自分の言葉で書き直したとき、それは Notes に昇格する。Clippings は素材のまま残り、出典として参照される。

#### Emails/ — コミュニケーションのアーカイブ

メールの記録。外部とのやり取りを Vault 内に統合し、検索可能にするための場所。自動同期で取り込む想定。

#### Generated/ — AI の作業場

AI が生成・維持するコンテンツ専用のフォルダ。あなたの思考（Notes/）と AI の生成物を明確に分離する。この区分が Think to Text Protocol の鍵でもある。人間が考えたものと、AI が作ったものは、混ぜない。

| サブフォルダ | 役割 |
|---|---|
| **Context/** | AI があなたの情報を整理・維持する思考設計図 |
| **Knowledge/** | AI が構築したナレッジベース |
| **Sessions/** | AI との対話セッションの記録 |
| **Logs/** | ツール操作のログ |

#### Libraries/ — Vault のインフラ

Vault を機能させるための裏方。普段は直接触らない。

| サブフォルダ | 役割 |
|---|---|
| **Templates/** | Templater のテンプレート。フォルダテンプレートで自動適用される |
| **Bases/** | Bases プラグインのビュー定義（`.base`）。各カテゴリの Table/Cards ビュー |
| **Categories/** | カテゴリのインデックスページ。`categories` プロパティのリンク先 |
| **Binaries/** | 添付ファイル（画像等）の保存先 |

### ノートの昇格フロー

```
Inbox（走り書き）→ Notes（自分の言葉で咀嚼した思考）
```

出典依存を外し、自分の言葉で咀嚼した思考になったとき、Inbox から Notes に昇格する。Clippings も同様に、咀嚼すれば Notes になる。昇格しなかったものはそのまま残る。捨てる必要はない。

## セットアップ

### 1. リポジトリをクローン

```bash
git clone https://github.com/yourname/skeleton-kamukafu-obsidian.git my-vault
```

### 2. Obsidian で開く

Obsidian を起動し、「Open folder as vault」で `my-vault` を選択。

### 3. コミュニティプラグインをインストール

Settings → Community plugins → Browse から以下をインストール：

- **Templater** — テンプレートエンジン（フォルダテンプレートで自動適用）
- **Tasks** — タスク管理（カスタムステータス付き）
- **Linter** — Markdown 整形（`created`/`updated` の自動管理）

設定は `.obsidian/plugins/` に含まれているため、プラグインをインストールすれば自動で反映される。

### 4. author を変更

テンプレート内の `yourname` を自分の名前に置換する：

```bash
# macOS / Linux
find Libraries/Templates -name "*.md" -exec sed -i '' 's/yourname/your-actual-name/g' {} +

# または手動で Libraries/Templates/*.md を編集
```

### 5. 書き始める

Daily Notes のショートカット（デフォルト: Cmd+N）で今日の日誌を作成し、書き始める。

## プラグイン設定の概要

### Templater（フォルダテンプレート）

フォルダにファイルを作成すると、対応するテンプレートが自動適用される：

| フォルダ | テンプレート |
|---|---|
| Notes/ | NoteTemplate.md |
| Inbox/ | InboxTemplate.md |
| Projects/ | ProjectTemplate.md |
| References/ | ReferenceTemplate.md |
| Generated/Sessions/ | SessionTemplate.md |

### Tasks（カスタムステータス）

Dataview フォーマットを採用。標準の `[ ]` / `[x]` に加え、以下のカスタムステータスが使える：

| 記法 | 意味 |
|---|---|
| `[/]` | In Progress（進行中） |
| `[-]` | Cancelled（キャンセル） |
| `[>]` | Rescheduled |
| `[<]` | Scheduled |
| `[!]` | Important |
| `[?]` | Question |
| `[*]` | Star |
| `[I]` | Idea |

### Linter

保存時に自動整形。主な設定：

- `created` / `updated` プロパティを `YYYY-MM-DD` 形式で自動管理
- ファイル名をヘッディングに自動設定
- Markdown 記法の統一（リストマーカー、引用、強調等）

### Bases

各カテゴリのビュー定義が `Libraries/Bases/` に `.base` ファイルとして配置されている。Obsidian の Bases コアプラグインで Table / Cards ビューとして表示される。

## ファイル命名規則

| フォルダ | パターン | 例 |
|---|---|---|
| Notes/ | 概念名 | `AiWorkflow.md`, `疎結合設計.md` |
| References/ | パスカルケース | `AndyMatuschak.md` |
| Daily/ | `YYYY-MM-DD.md` | `2026-03-16.md` |
| Projects/ | フォルダ名パスカルケース | `Projects/MyProject/` |

## AI との統合

この Vault は AI（Claude Code 等）との協働を前提に設計されている。

- **Generated/** フォルダは AI 専用の作業場。あなたの思考（Notes/）と AI の生成物を明確に分離する
- **author / editor** プロパティで、誰が書いたかを常に追跡する
- **プレーンテキスト**（Markdown）であるため、AI が直接読み書きできる
- **CLAUDE.md** を Vault ルートに置くことで、Claude Code に Vault の構造と規約を教える

## ライセンス

MIT

## クレジット

- [Obsidian](https://obsidian.md/) — kepano (Steph Ango)
- [Evergreen Notes](https://notes.andymatuschak.org/Evergreen_notes) — Andy Matuschak
- [File over app](https://stephango.com/file-over-app) — Steph Ango
- Think to Text Protocol（かむかふプロトコル）— Akiomi Kuroda
