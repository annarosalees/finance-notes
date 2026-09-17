---

description: "Task list template for feature implementation"
---

# Tasks: FXノート（`notes/fx.md`）の新規作成

**Input**: Design documents from `/specs/001-fx-note/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, quickstart.md
（本featureにcontracts/は存在しない — 外部インターフェースを持たない
Markdownドキュメントのfeatureのため）

**Tests**: 自動テストは対象外（spec.mdで明示的に要求されていないため）。
代わりに quickstart.md の手動検証手順を Polish フェーズで実行する。

**Organization**: タスクはspec.mdのUser Story（P1/P2/P3）ごとにグループ
化されている。各ストーリーは `notes/fx.md` の対応セクションを執筆する
ことで独立して検証できる。

## Format: `[ID] [P?] [Story] Description`

- **[P]**: 並行実行可能（異なるファイル、他タスクへの依存なし）
- **[Story]**: どのUser Storyに属するか（US1, US2, US3）
- 各タスクには具体的なファイルパスを含む

## Path Conventions

本リポジトリはアプリケーションコードを持たないため、`src/`/`tests/` は
存在しない。すべてのタスクは `notes/`, `README.md`, `README.en.md` を
対象とする（plan.mdのProject Structureを参照）。

---

## Phase 1: Setup（ファイル雛形の作成）

**Purpose**: 4部構成の見出しだけを持つ空のノートファイルを用意する
（data-model.md「セクション構成」）

- [X] T001 `notes/fx.md` を新規作成し、4つの `##` 見出し
      （商品概要／価格・損益の仕組み／実務上どのように扱われるか／
      つまずきやすいポイント）のみを持つ雛形を作成する（FR-001）
- [X] T002 [P] `notes/fx.en.md` を新規作成し、`notes/fx.md` と対応する
      英語見出し（What FX Is / How Price and P&L Work / How It's Handled
      in Practice / Common Pitfalls 等）のみを持つ雛形を作成する
      （FR-008, SC-004）

**Checkpoint**: 2ファイルとも4見出しの雛形が揃い、以降のUser Story
フェーズで本文を追記できる状態になる。

*Phase 2 (Foundational) は本featureでは不要 — Setupで作成した雛形が
全User Storyの前提を兼ねるため。*

---

## Phase 3: User Story 1 - FXの仕組みを基礎から理解する (Priority: P1) 🎯 MVP

**Goal**: 読者が `notes/fx.md` を読み、FXがCFDの一種であること、および
pips・レバレッジ・証拠金・スワップポイントの意味を理解できる。

**Independent Test**: `notes/fx.md` 単体を読み、「CFDとの関係」「pips」
「レバレッジ」「証拠金」「スワップポイント」を他のノートを参照せずに
説明できるかで検証する。

### Implementation for User Story 1

- [X] T003 [US1] `notes/fx.md` の「商品概要」節（見出し1）に、FXがCFD
      の一種（通貨ペアを対象にした差金決済取引）であることを明記し、
      `notes/cfd.md` への相対リンクを追加する（FR-002, data-model.md
      「セクション1」）
- [X] T004 [US1] `notes/fx.md` の「価格・損益の仕組み」節（見出し2）に、
      pips・レバレッジ・証拠金・スワップポイントの4用語を、専門知識の
      ない読者にも分かる言葉で説明する（FR-003, SC-001, constitution
      原則V）
- [X] T005 [US1] `notes/fx.en.md` の対応する2見出し（What FX Is /
      How Price and P&L Work）に、T003・T004と同じ内容量の英語版を
      執筆し、`notes/cfd.en.md` への相対リンクを追加する。日本語版に
      対して部分的にしか訳せない場合は該当箇所に未翻訳である旨を明示
      する（FR-008, constitution原則I）

**Checkpoint**: この時点で `notes/fx.md`／`notes/fx.en.md` の前半2節が
完成し、User Story 1 は単体で検証可能。

---

## Phase 4: User Story 2 - 実務上の扱い（レート生成・カバー）を理解する (Priority: P2)

**Goal**: 読者がFXレートの生成方法とカバーディールの目的を理解できる。

**Independent Test**: 「実務上どのように扱われるか」節だけを読み、レー
ト生成とカバーディールの基本的な流れを自分の言葉で説明できるかで検証
する。

### Implementation for User Story 2

- [X] T006 [US2] `notes/fx.md` の「実務上どのように扱われるか」節
      （見出し3）に、インターバンクレートを基にした社内レート生成の考
      え方と、カバーディールの目的（在庫リスクの調整）を説明する
      （FR-004, data-model.md「セクション3」）
- [X] T007 [US2] `notes/fx.en.md` の対応する見出し（How It's Handled in
      Practice）に、T006と同じ内容量の英語版を執筆する。日本語版に対し
      て部分訳になる場合は未翻訳部分を明示する（FR-008）

**Checkpoint**: User Story 1・2の内容が揃い、前半3節が両言語で完成。

---

## Phase 5: User Story 3 - つまずきやすいポイントを事前に把握する (Priority: P3)

**Goal**: 読者がFX特有の誤解しやすいポイントを事前に把握できる。

**Independent Test**: 「つまずきやすいポイント」節のみを読み、少なくと
も3つの誤解しやすいポイントを挙げられるかで検証する。

### Implementation for User Story 3

- [X] T008 [US3] `notes/fx.md` の「つまずきやすいポイント」節（見出し4）
      に、少なくとも3件の注意点（スワップポイントが正負どちらにもなり
      得ること／国内FX業者のレバレッジ規制（最大25倍等、法改正等によ
      る変更可能性の注記付き）／週明け窓開けリスク）を記載する
      （FR-005, SC-003, spec Assumptions）
- [X] T009 [US3] `notes/fx.en.md` の対応する見出し（Common Pitfalls）
      に、T008と同じ3件以上の注意点を英語で記載する（FR-008）

**Checkpoint**: `notes/fx.md`／`notes/fx.en.md` の4節すべてが両言語で
完成し、全User Storyが独立に検証可能になる。

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: 全体の整合性確認とREADME更新

- [X] T010 [P] `notes/fx.md` と `notes/fx.en.md` の `##` 見出しの数・
      順序が一致していることを確認する（例:
      `grep -n "^##" notes/fx.md notes/fx.en.md` で突き合わせ）
      （FR-008, SC-004）
- [X] T011 `notes/fx.md`・`notes/fx.en.md` に特定企業・システムの内部
      情報や断定的な売買推奨表現が含まれていないことを確認する
      （FR-006, FR-007, constitution原則III・IV）
- [X] T012 [P] `README.md` の「収録ノート」欄で `notes/fx.md` の記載を
      `` `notes/fx.md` … FX（外国為替証拠金取引）※作成予定 `` から
      `` [`notes/fx.md`](./notes/fx.md) … FX（外国為替証拠金取引） ``
      （リンク付き・「※作成予定」を削除）に更新する（FR-009）
- [X] T013 [P] `README.en.md` の対応する行を、日本語版と同じ方針で
      「作成予定」表記からリンク付きの表記に更新する（FR-009）
- [X] T014 `specs/001-fx-note/quickstart.md` の検証手順1〜7をすべて実行
      し、期待結果を満たすことを確認する

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: 依存なし。T001とT002は並行可能。
- **User Story 1 (Phase 3)**: Setup完了後に開始可能。T003→T004の順（同
  一ファイル内の別セクションだが、商品概要が先にあることでCFDとの関係
  性の前提がT004の説明にも活きるため）。T005はT003・T004完了後（翻訳の
  ため）。
- **User Story 2 (Phase 4)**: Setup完了後に開始可能。US1と内容的に独立
  だが、同じファイル（`notes/fx.md`, `notes/fx.en.md`）を編集するため、
  マージの都合上US1完了後に着手することを推奨。
- **User Story 3 (Phase 5)**: 同様にSetup完了後に開始可能。US1・US2完了
  後の着手を推奨。
- **Polish (Phase 6)**: すべてのUser Story完了後。

### User Story Dependencies

- **User Story 1 (P1)**: 他ストーリーへの依存なし。MVP。
- **User Story 2 (P2)**: US1への依存なし（内容的に独立）。ただし同一
  ファイルを扱うため実行順としてはUS1の後を推奨。
- **User Story 3 (P3)**: US1・US2への依存なし（内容的に独立）。実行順
  としては最後を推奨。

### Parallel Opportunities

- T001とT002（ja/en雛形作成）は並行可能。
- T012とT013（README.md/README.en.mdの更新）は並行可能。
- T010（見出し一致確認）はT012/T013と並行可能。
- 同一ファイル（`notes/fx.md`, `notes/fx.en.md`）を編集するタスク同士は
  競合を避けるため並行実行しない。

---

## Parallel Example: Setup

```bash
# T001とT002は異なるファイルなので並行実行可能:
Task: "notes/fx.md に4見出しの雛形を作成"
Task: "notes/fx.en.md に対応する4見出しの雛形を作成"
```

## Parallel Example: Polish

```bash
# T012とT013は異なるファイルなので並行実行可能:
Task: "README.md の収録ノート欄を更新"
Task: "README.en.md の収録ノート欄を更新"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Phase 1 (Setup) を完了する
2. Phase 3 (User Story 1) を完了する
3. **STOP and VALIDATE**: `notes/fx.md` の前半2節だけを読んで independent
   testを満たすか確認する
4. ここまでで「FXとは何か」を理解できるMVPが完成

### Incremental Delivery

1. Setup → 雛形完成
2. User Story 1 → 検証 → （必要なら途中経過として共有）
3. User Story 2 → 検証
4. User Story 3 → 検証
5. Polish（見出し一致確認・禁止事項確認・README更新・quickstart実行）
   → featureとして完了

---

## Notes

- [P] タスク = 異なるファイル、依存関係なし
- [Story] ラベルはトレーサビリティのためUser Storyに対応付ける
- 各User Storyは独立して完結・検証可能であること
- 論理的な単位ごとにコミットする
- 各チェックポイントでストーリー単体の検証を行う
- 避けるべきこと: 曖昧なタスク、同一ファイルへの競合する並行編集、
  ストーリー間の独立性を壊す依存関係
