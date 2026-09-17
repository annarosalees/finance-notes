# Phase 0 Research: FXノート（`notes/fx.md`）

Technical Contextに `NEEDS CLARIFICATION` はなし（ドキュメントのみの
featureのため技術選定は不要）。本ドキュメントは、執筆にあたって参照すべき
既存資産と内容方針を整理する。

## R1: 参照すべき既存ノートの構成

- **Decision**: `notes/cfd.md` の4部構成（商品概要／価格・損益の仕組み
  ／実務上の扱い／つまずきやすいポイント）を見出しレベルの型として踏襲
  する。ただし `notes/fx.md` は新規なので、`cfd.md` にある「目次」節や
  ロールオーバー特有の節は模倣せず、spec.mdのUser Story 1〜3にそのまま
  対応する4見出しとする。
- **Rationale**: constitution原則IIで4部構成が固定されており、
  `cfd.md` が唯一の完成済み前例のため。
- **Alternatives considered**: `cfd.md` の見出し階層（`##`/`###`/`####`
  混在）をそのまま複製する案は採用せず、fxノートでは4つの `##` 見出しに
  フラットに揃える（spec FR-001〜005が4節を明確に要求しているため、
  階層を増やすと日英対応の検証（SC-004）が複雑になる）。

## R2: FXとCFDの関係の説明方法

- **Decision**: `notes/fx.md` 冒頭（商品概要節）で「FXはCFDの一種（通貨
  ペアを対象にした差金決済取引）」と明示し、`notes/cfd.md` への相対リン
  ク（`[CFDノート](./cfd.md)`）を張る。英語版も同様に `[CFD note](./cfd.en.md)`
  を張る。
- **Rationale**: spec Edge Casesで「`cfd.md`未読の読者でも関係が分かる
  こと」が要求されているため。
- **Alternatives considered**: CFDノート側からFXノートへの逆リンクを追
  加する案は、本specのスコープ外（`cfd.md`の変更は本featureに含まれない）
  として見送る。

## R3: 英語版の翻訳範囲

- **Decision**: 初版から日本語版と同じ4節構成・同等の情報量で作成する
  （`cfd.en.md` で生じている「部分訳」の乖離を今回は繰り返さない）。
  やむを得ず一部を省略する場合は、該当節に `<!-- TODO: 未翻訳 -->` 等の
  形で明示する。
- **Rationale**: spec Edge Casesおよびconstitution原則Iより。
- **Alternatives considered**: 日本語版を先に完成させ英語版は骨子のみに
  する案は、原則I違反のリスクが高いため不採用。

## R4: レバレッジ規制等の数値の扱い

- **Decision**: 「国内FX業者は個人向け最大25倍」等、一般的な制度として
  記載し、「法改正等により変更されうる」旨の注記を添える。特定の業者名
  は挙げない。
- **Rationale**: spec Assumptions、constitution原則III・IVより。
- **Alternatives considered**: 数値を一切出さない案は、SC-003（つまずき
  ポイントの具体性）を満たしにくいため不採用。

## R5: 図表（`assets/`）の要否

- **Decision**: 本feature（初版執筆）では図表なしのテキストのみで4部構
  成を満たせると判断し、tasksフェーズでは図表タスクを起こさない。将来
  必要になった場合は別featureとして追加する。
- **Rationale**: `cfd.md` も現状テキストのみで完結しており、pips・レバ
  レッジ・スワップは文章での説明で足りると判断できるため。
- **Alternatives considered**: 為替レートとpipsの関係を図示する案は、
  スコープを広げるため今回は見送り。

すべてのNEEDS CLARIFICATIONは解消済み。Phase 1に進む。
