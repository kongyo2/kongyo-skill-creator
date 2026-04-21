---
name: kongyo-skill-creator
description: "Create or refactor a Codex/Claude skill into kongyo-style operational documentation: explicit trigger text, first-screen quickstart, decision tables, copy-paste templates, pitfalls, troubleshooting, and a clean split between SKILL.md, references/, and assets/. Use when authoring a new skill, rewriting an explanation-heavy skill into an executable runbook, standardizing team skill structure, or reviewing whether a skill is practical enough to run without guesswork."
---

# Kongyo Skill Creator

`kongyo` 系 skill の強みは「知識の説明」ではなく「その場で動ける運用メモ」にある。最初の 1 画面で何をすればいいかが分かり、分岐基準と失敗時の戻り方が見え、必要なら `references/` と `assets/` に深掘りできる形へ整える。

## いつ使うか

- 新規 skill を作るが、実行手順・判断基準・落とし穴まで含めたいとき
- 既存 skill が説明中心で、現場でそのまま使えないとき
- 複数の skill を同じ書き味に寄せたいとき
- `description` の trigger、section 順序、テンプレ資産の切り出し方を見直したいとき

使わない場面:
- 一回限りのメモ
- API 仕様を保管するだけの資料
- 既に短く完結していて、分岐も再利用資産もない skill

## 最初に読むもの

- `references/kongyo-skill-patterns.md`
  `kongyo` 系 skill を 3 archetype に分類している。まずこれで寄せる型を決める。
- `references/review-checklist.md`
  仕上げ前の品質ゲート。trigger 明確性、初速、分岐、コピペ性、事故防止を採点する。

## 出力契約

最低でも次を満たす。

| 項目 | 必須条件 |
|---|---|
| Frontmatter | `name` は kebab-case、`description` だけで trigger が判断できる |
| First screen | 先頭 1 画面で「いつ使うか」「最短成功パス」「必要入力」が読める |
| Decision support | 分岐が 2 つ以上あるなら table または `if ... then ...` を置く |
| Reuse | コマンド、プロンプト、設定例、テンプレのいずれかを 1 つ以上置く |
| Failure handling | 3 件以上の落とし穴、または troubleshooting を置く |
| Disclosure | 長い詳細は `references/`、コピーして使う雛形は `assets/` に逃がす |

必要に応じて次も追加する。

- `references/`: variant ごとの詳細、長い API/CLI 補足、評価軸、比較表
- `assets/`: 雛形ファイル、最小プロジェクト、設定例、画像・アイコン
- `scripts/`: 同じコードを何度も書くか、手動では壊しやすい処理があるとき

## Archetype を決める

primary archetype を 1 つ決めてから書く。hybrid は許容するが、初速を支配するのは 1 つに絞る。

| Archetype | 向いている skill | 最初に必要なもの | 典型的な追加資産 |
|---|---|---|---|
| Evaluator | レビュー、採点、再現性確認、style check | 評価軸、workflow、report template | rubric、dispatch prompt |
| Operations | 個人/チーム運用、日常手順、環境管理 | 前提環境、layout/table、日常フロー | command cheat sheet、troubleshooting |
| Practice | CLI / library / FFI / framework の実践ガイド | quickstart、原則、実例、decision table | `references/` の詳細 docs、`assets/` の starter |
| Meta | skill 作成、分類、提案、ふりかえり | 分類基準、出力契約、提案テンプレ | archetype 別 template、review checklist |

具体例は `references/kongyo-skill-patterns.md` を読む。

## Workflow

1. **ソースを監査する**
   次を抜き出す。
   - 誰が何を終えるための skill か
   - 最短成功パスは何か
   - どこで判断が分岐するか
   - 何を間違えると痛いか
   - 何を `assets/` や `references/` に切り出せるか

2. **primary archetype を決める**
   `Evaluator / Operations / Practice / Meta` のどれが中心かを先に決める。全部入りにしない。

3. **`SKILL.md` / `references/` / `assets/` の境界を切る**
   - `SKILL.md`: すぐ動くための手順、判断、注意点だけ残す
   - `references/`: variant 詳細、長い比較表、評価軸、公式情報の要約
   - `assets/`: そのままコピーしたい雛形や最小構成
   - `scripts/`: deterministic にしたい処理だけ

4. **frontmatter を先に確定する**
   `description` は次の式で書く。
   `What it does. Use when <task>, <symptom>, or <decision point>.`

   悪い例: `XX のガイド`
   良い例: `XX を設定・運用・トラブル調査するガイド。Use when 新規導入、既存設定の修正、または failure 原因調査を行うとき。`

5. **先頭 1 画面を作る**
   以下を優先順に置く。
   - `## いつ使うか`
   - `使わない場面`
   - quickstart か minimal workflow
   - 必要入力 / 前提環境

   抽象的な背景説明はこの後ろに回す。

6. **分岐と判断基準を書く**
   branch が 2 つ以上あるなら、table か `if ... then ...` を必ず入れる。
   判断が暗黙だと skill は trigger しても実行で詰まる。

7. **コピペ資産を置く**
   次のどれかを必ず 1 つ以上用意する。
   - コマンド列
   - dispatch prompt
   - 設定ファイル全文
   - 雛形 SKILL
   - 変更提案フォーマット

   placeholder を使うなら、何に置換するかも 1 行で明記する。

8. **落とし穴と戻り方を書く**
   `気をつける` だけで終わらせない。
   `誤り -> 実害 -> 回避策` か `症状 -> 原因 -> 打ち手` で書く。

9. **仕上げを検査する**
   `references/review-checklist.md` で採点する。

## 記述ルール

- 理屈より先に操作を書く
- 見出しは `読む順 = 作業順` に寄せる
- 断定できることは断定する
- 一般論より固有名詞、コマンド、ファイル名、しきい値を優先する
- section が長くなったら要約だけ `SKILL.md` に残し、詳細は `references/` に逃がす
- 複数 variant があるなら対称的な section を並べるより、decision table で入口を一本化する
- 関連 skill は「次に何を読むべきか」が自然なものだけ残す

## Quality Gate

`references/review-checklist.md` の合格条件を満たすまで出さない。

- 合計 12/16 以上
- `Trigger clarity`, `First-screen success path`, `Decision support`, `Failure handling` の 4 軸で 0 点を出さない
- `references/` や `assets/` を追加した場合は、`SKILL.md` から直接たどれる状態にする

## Red Flags

- `description` が「ガイド」「ベストプラクティス」だけで終わっている
- quickstart が理屈の後ろに埋もれている
- branch があるのに decision table がない
- テンプレが抽象的で、コピペしても動かない
- `references/` に逃がしたのに `SKILL.md` から読みに行く条件が書かれていない
- 落とし穴が `注意する` `確認する` で終わる
- archetype を混ぜすぎて、最初の見出し順が作業順になっていない
