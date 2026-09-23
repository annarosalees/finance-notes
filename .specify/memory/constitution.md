<!--
Sync Impact Report
- Version change: 1.2.0 → 1.2.1 (PATCH: clarification, no new principle)
- Modified principles:
  - VII. 本文執筆の主体 (User Owns the Writing) — added one clarifying paragraph:
    names `study-issue` skill as the primary source for what counts as an explicit
    drafting request, and describes its two operating modes (「一緒に進めて」 =
    draft-and-confirm co-writing cycle; plain issue-start instructions = wall-bounce
    only, no drafting). Resolves an apparent tension surfaced during live testing on
    issue #61, where a strict no-draft interpretation proved too rigid for the
    learning workflow the user actually wants.
- Added sections: none
- Removed sections: none
- Follow-up TODOs: none
-->
# finance-notes Constitution

## Core Principles

### I. バイリンガル整合性 (Bilingual Parity)
すべてのノートは日本語版（`notes/*.md`）と英語版（`notes/*.en.md`）を対で維持する。
英語版は日本語版の要約ではなく、同じセクション構成・同等の情報量を持つ翻訳とする。
日本語版を更新した場合は、同じ変更を英語版にも反映する（またはTODOとして明示する）まで
そのノートは「完了」とみなさない。

### II. 共通ノート構成の遵守 (Fixed Note Structure)
すべてのノートはREADMEで定義された4部構成に従う:
1. その商品は何か
2. どのような仕組みで価格・損益が決まるか
3. 実務上どのように扱われるか（レート生成・カバー等の観点）
4. つまずきやすいポイント
この構成を変更する場合は、READMEとconstitutionの両方を更新する。

### III. 機密情報の排除 (No Proprietary Information)
特定の企業・システムの内部情報（社内システム名、非公開の運用フロー、契約条件等）は
一切含めない。一般的な業界慣行・公開情報の範囲でのみ記述する。

### IV. 非助言性 (Not Investment Advice)
本リポジトリの全コンテンツは個人的な学習記録であり、投資助言を目的としない。
売買判断を促すような断定的表現（「買うべき」「今が買い時」等）は避ける。

### V. 平易な説明 (Accessible Explanations)
専門用語に頼りすぎず、実務未経験者にも理解できる説明を優先する。専門用語を使う場合は
初出時に簡潔な補足を添える。

### VI. 対話的な進行 (Guided, Step-by-Step Process)
本リポジトリは成果物だけでなく学習プロセスそのものを重視する。新しい内容（ノートの
セクション、spec-kitの各コマンド等）に着手する前に、それが何か・なぜ必要かを説明し、
ユーザーの合意を得てから進める。一度に多くの項目を進めず、1項目ずつ確認しながら進め
る。`/speckit-implement` のように複数タスクを一括実行するコマンドは、ユーザーが範囲
を明示的に許可した場合にのみ使い、全タスクの自動実行をデフォルトにしない。不明点は
想像で埋めず、ユーザーに確認する。ノート本文の執筆に関する進行方法は原則VIIに従う。

### VII. 本文執筆の主体 (User Owns the Writing)
`notes/*.md`（および対となる`notes/*.en.md`）の本文の新規執筆・書き足しは、ユーザー
自身が行う。これはユーザーが自分の言葉で理解を書き出すという本リポジトリの学習目的
そのものであり、Claude・spec-kitのワークフロー（`/speckit-implement`等のタスク一括
実行コマンドを含む）・および本文執筆を支援する目的で作られるスキルやコマンドは、
ユーザーから明示的に「代わりに書いて」と依頼されない限り、セクションの文章を書いて
コミットしてはならない。Issue（学習トピック）や目次を見て「代わりに書いておきました」
と先回りして進めることも禁止する。
これらのツール・ワークフローに許される役割は次の3つに限定される：
1. **壁打ち**：ユーザーが書こうとしている内容について、理解を確認する質問を投げる
   （答えを直接言わず、気づきを促す）。
2. **不足の指摘**：説明として足りない部分・論理が飛んでいる部分を指摘する
   （正解は言わず、考え直すきっかけを与える）。
3. **軽い添削**：誤字脱字・言い回しの軽い修正は提案してよい。ただし新しい段落や
   具体例を丸ごと書き足すことはしない。
ただし、事実の誤りは壁打ちの対象にせず、はっきり誤りと正解を伝える。金融知識として
誤った内容がノートに残ることは、学習目的よりも優先して防止する。
「ユーザーから明示的に代筆を依頼された」場合の具体的な運用は `study-issue` スキル
（`.claude/skills/study-issue/SKILL.md`）が一次情報源となる。同スキルが定義する
「一緒に進めて」形式の依頼は、観点ごとにユーザーの口頭説明を聞いた上でドラフトを
提示し、確認・修正を経て確定するサイクルであり、これ自体が本原則の言う明示的な
代筆依頼にあたる。この形式の依頼がない、単なる着手指示（「issueに進む」等）の場合は、
上記3役（壁打ち・不足の指摘・軽い添削）に限定したモードで進める。

## 追加制約

- 本リポジトリにはアプリケーションコード・ビルド・CIは存在しない。ノート追加はMarkdown
  ファイルの追加・編集のみで完結する。
- 図表・画像は `assets/` 配下に置き、ノート本文からの相対リンクで参照する。

## 開発ワークフロー

- 新しいノート（例: `notes/fx.md`）を追加する際は spec-kit のワークフロー
  （`/speckit-specify` → `/speckit-plan` → `/speckit-tasks` → `/speckit-implement`）に従い、
  着手前にspecでノートの対象読者・記述範囲・完了基準を明確化する。
- `/speckit-implement` を実行する際も、原則VI（対話的な進行）に従い、タスクを区切って
  ユーザーと合意を取りながら進める。全タスクを無条件に自動実行しない。タスクに
  「ノートに〜を追加する」等の本文執筆が含まれる場合は、原則VII（本文執筆の主体）に
  従い、Claudeがタスクを消化する形で本文を書いてはならない。
- specの「User Scenarios」は「読者がこのノートを読んで何を理解・判断できるようになるか」、
  「Functional Requirements」は「ノートが満たすべき記述項目」として記述する。

## Governance

本constitutionはREADME.mdの記載事項と矛盾しないものとし、矛盾が生じた場合は両方を
同時に更新する。原則の追加・変更は、変更理由をコミットメッセージに明記した上で行う。

**Version**: 1.2.1 | **Ratified**: 2026-09-16 | **Last Amended**: 2026-09-23
