# Implementation Plan: FXノート（`notes/fx.md`）の新規作成

**Branch**: `001-fx-note` | **Date**: 2026-09-17 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/001-fx-note/spec.md`

## Summary

README で「作成予定」と予告されている `notes/fx.md`（日本語版）と
`notes/fx.en.md`（英語版）を、`notes/cfd.md` と同じ4部構成
（商品概要／価格・損益の仕組み／実務上の扱い／つまずきやすいポイント）
で新規執筆する。技術的な実装は伴わず、Markdownドキュメント2本の追加と、
`README.md`／`README.en.md` の「収録ノート」欄の更新のみで完結する。

## Technical Context

**Language/Version**: N/A（Markdownドキュメントのみ、アプリケーション
コードなし）

**Primary Dependencies**: N/A

**Storage**: ファイルベース（`notes/fx.md`, `notes/fx.en.md` をリポジト
リに追加）

**Testing**: 自動テストなし。人手によるレビュー（4部構成の充足、日英の
見出し対応、constitution原則I〜Vとの整合）で検証する。

**Target Platform**: GitHub上でのMarkdown閲覧

**Project Type**: ドキュメントリポジトリ（single project、コードなし）

**Performance Goals**: N/A

**Constraints**:
- 4部構成（constitution原則II）を厳守すること
- 日英の見出し構成を一致させること（constitution原則I）
- 特定企業・システムの内部情報を含まないこと（constitution原則III）
- 断定的な売買推奨表現を含まないこと（constitution原則IV）
- 専門用語は初出時に補足すること（constitution原則V）

**Scale/Scope**: ノート2本（`notes/fx.md`, `notes/fx.en.md`）＋
README.md／README.en.mdの該当行更新

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- **原則I（バイリンガル整合性）**: PASS — 日英を対で作成し、見出し構成
  を一致させる方針（FR-008）。英訳が部分的な場合は明示する。
- **原則II（共通ノート構成）**: PASS — 4部構成をそのまま踏襲
  （FR-001〜FR-005）。
- **原則III（機密情報の排除）**: PASS — 一般的な業界慣行の範囲に限定
  （FR-006）。
- **原則IV（非助言性）**: PASS — 断定的売買推奨表現を含めない
  （FR-007）。
- **原則V（平易な説明）**: PASS — pips・レバレッジ等の専門用語は初出時
  に補足する（SC-001）。
- **追加制約（アプリコード・CIなし）**: PASS — Markdown追加のみ。
- **追加制約（図表は`assets/`配下）**: 該当する場合のみ適用。図表要否は
  tasksフェーズで判断（spec Assumptions）。

違反なし。Complexity Trackingは不要。

## Project Structure

### Documentation (this feature)

```text
specs/001-fx-note/
├── plan.md              # This file (/speckit-plan command output)
├── research.md          # Phase 0 output (/speckit-plan command)
├── data-model.md        # Phase 1 output (/speckit-plan command)
├── quickstart.md        # Phase 1 output (/speckit-plan command)
├── contracts/           # Phase 1 output (N/A — 外部インターフェースなし)
└── tasks.md             # Phase 2 output (/speckit-tasks command)
```

### Source Code (repository root)

```text
notes/
├── cfd.md               # 既存（参照する構成のお手本）
├── cfd.en.md             # 既存
├── fx.md                 # 新規作成（このfeatureの成果物）
└── fx.en.md               # 新規作成（このfeatureの成果物）

README.md                 # 「収録ノート」欄を更新
README.en.md               # 「収録ノート」欄を更新
```

**Structure Decision**: 本プロジェクトはアプリケーションコードを持たない
Markdownドキュメントリポジトリのため、`src/`や`tests/`に相当する構造は
存在しない。既存の `notes/` 直下にファイルを追加する単一構成
（Option 1相当だが実体はドキュメントのみ）を採用する。

## Complexity Tracking

*本featureにConstitution Check違反はないため、このセクションは空欄。*
