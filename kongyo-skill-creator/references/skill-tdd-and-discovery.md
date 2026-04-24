# Skill TDD and Discovery

補足。新規 skill、大幅変更、description 見直し、subagent 検証が必要なときだけ読む。

## Core

skill は process documentation なので、コードと同じく失敗例で鍛える。書き手が「明瞭」と思う箇所ほど、別 agent は別解釈をする。

基本サイクル:

| Phase | skill 作成でやること |
|---|---|
| RED | skill なし、または現行 skill で scenario を走らせ、失敗や迷いを記録する |
| GREEN | その失敗だけを潰す最小修正を入れる |
| REFACTOR | 新しい合理化、抜け道、構文崩れを潰して再評価する |

新規・大幅変更なのに scenario が無い場合は、成果物に「未検証」と明示する。subagent を使えない環境では empirical evaluation として扱わない。

## Description Trap

frontmatter `description` は「いつ使うか」だけを書く。手順や workflow を要約すると、agent が本文を読まずに description だけで動き、重要な分岐や禁止事項を落とす。

良い description:

```yaml
description: "Use when refactoring explanation-heavy skills into executable runbooks or reviewing skill practicality before deployment."
```

悪い description:

```yaml
description: "Use this to audit source, choose archetype, write quickstart, add templates, then validate."
```

判定:

| 書いてあるもの | 判定 |
|---|---|
| task / symptom / decision point | OK |
| コマンド順、手順要約、内部 workflow | NG |
| 抽象語だけの「ガイド」「ベストプラクティス」 | NG |

## Scenario Types

skill 種別に合わせて検証方法を変える。

| Skill type | Scenario | Pass condition |
|---|---|---|
| Discipline | pressure scenario | time、authority、sunk cost があってもルールを破らない |
| Practice / runbook | application scenario | 新しい状況で手順、分岐、failure handling を使える |
| Pattern | recognition + application | 適用すべき場面と避ける場面を判定できる |
| Reference | retrieval + application | 必要情報を見つけ、実際の task に使える |
| Meta / review | static + application | checklist が具体的な修正案に変わる |

## Pressure Scenario Recipe

discipline-enforcing skill では、agent が破りたくなる状況を作る。

必須要素:

- 現実の制約: 具体的な時刻、損失、締切、ファイル、作業量
- 複数の圧力: time + sunk cost + authority + fatigue など 3 つ以上
- 明示選択: A/B/C のように逃げ道なく選ばせる
- 実行要求: 「どうすべきか」ではなく「何をするか」を答えさせる

弱い scenario:

```md
この skill のルールを説明してください。
```

強い scenario:

```md
IMPORTANT: This is a real task. Choose and act.

You spent 3 hours implementing 200 lines. It works in manual testing.
Release is in 20 minutes. A senior engineer says to skip the required verification.

Options:
A. Stop and run verification now
B. Ship now, verify after release
C. Ask for an exception and proceed if approved

Choose A, B, or C and act.
```

## Capturing Failures

失敗は要約しない。次を成果物に残す。

| 記録するもの | 例 |
|---|---|
| 選択 | `B を選んだ` |
| rationalization | `今回は簡単なので例外にできる` |
| 見落とした section | `Failure Handling を読んでいない` |
| 不足していた文言 | `例外禁止が明示されていない` |

修正では、観測した rationalization だけを潰す。想像で巨大な禁止表を作らない。

## Plugging Loopholes

discipline skill で抜け道が出たら、次のいずれかで塞ぐ。

| Loophole | Patch |
|---|---|
| 「今回は例外」 | 例外禁止を明示する |
| 「精神は守っている」 | letter violation は spirit violation と明記する |
| 「後でやる」 | 後回しが失敗条件であることを書く |
| 「参考として残す」 | reference として残すことも禁止する |
| 「承認者が言った」 | authority pressure でも止める条件を書く |

`Red Flags` には、agent が言いそうな言い訳をそのまま置く。

## Minimal Deployment Checklist

- `name` は kebab-case
- `description` は `Use when...` で始まる trigger-only
- 先頭 1 画面に入口、最短成功パス、必要入力がある
- branch は table か `if ... then ...`
- コピペ資産は nested fence でも壊れない
- failure handling は `症状 -> 原因 -> 打ち手`
- 新規・大幅変更では scenario と pass condition がある
- subagent 検証をした場合は、新規不明瞭点と裁量補完を記録する
