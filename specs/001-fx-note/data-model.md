# Phase 1 Data Model: FXノート（`notes/fx.md`）

本featureはソフトウェアのデータモデルを持たない（アプリケーションコー
ドなし）。代わりに、ノートというドキュメントの構造を「エンティティ」と
して整理する。

## Entity: FXノート（`notes/fx.md` / `notes/fx.en.md`）

| 属性 | 説明 | 検証ルール |
|---|---|---|
| ファイルパス | `notes/fx.md`（日本語版）／`notes/fx.en.md`（英語版） | 両方が存在すること（FR-008） |
| セクション構成 | 4部構成の見出し（`##`） | FR-001〜005: 4節すべてが存在し、プレースホルダでない本文を持つこと（SC-002） |
| セクション1: 商品概要 | FXがCFDの一種であることの説明＋`cfd.md`/`cfd.en.md`への相互リンク | FR-002 |
| セクション2: 価格・損益の仕組み | pips／レバレッジ／証拠金／スワップポイントの4用語の説明 | FR-003, SC-001 |
| セクション3: 実務上の扱い | インターバンクレートを基にした社内レート生成＋カバーディールの説明 | FR-004 |
| セクション4: つまずきやすいポイント | 誤解しやすい点を3件以上 | FR-005, SC-003 |
| 日英対応 | 見出しの数・順序が日英で一致 | FR-008, SC-004 |
| 禁止事項 | 特定企業・システムの内部情報を含まない／断定的売買推奨表現を含まない | FR-006, FR-007 |

## Relationship

- `notes/fx.md` **references** `notes/cfd.md`（相互リンク、R2）
- `notes/fx.en.md` **references** `notes/cfd.en.md`
- `README.md` / `README.en.md` の「収録ノート」欄 **links to**
  `notes/fx.md` / `notes/fx.en.md`（FR-009、本featureのtasksで対応）

## State

ノートに状態遷移はない（一度公開された静的ドキュメント）。ただし
README上の表記は以下の2状態を取り、本featureで前者から後者へ遷移する：

1. `notes/fx.md` … FX（外国為替証拠金取引）※作成予定
2. [`notes/fx.md`](./notes/fx.md) … FX（外国為替証拠金取引）
