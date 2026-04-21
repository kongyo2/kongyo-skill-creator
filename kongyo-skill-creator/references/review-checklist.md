# Review Checklist

`kongyo-skill-creator` で作った skill を出す前に使う静的チェック。

## Scoring

各軸を 0-2 点で採点する。合計 16 点満点。

| 軸 | 0 | 1 | 2 |
|---|---|---|---|
| Trigger clarity | `description` が曖昧で trigger しない | what か when の片方だけある | what + when + 具体的な task / symptom がある |
| First-screen success path | 先頭に操作が無い | 使いどころはあるが動き出しが遅い | 1 画面目で最短成功パスに入れる |
| Inputs / prerequisites | 必要環境が不明 | 一部だけ書いてある | 必要入力、前提、対象範囲が見える |
| Decision support | 分岐が暗黙 | 箇条書きで説明だけある | table か `if ... then ...` で分岐が固定されている |
| Copy-paste assets | そのまま使える素材が無い | 一部だけコピペできる | コマンド / prompt / file template をそのまま使える |
| Failure handling | 落とし穴が無い | 注意はあるが抽象的 | `症状 -> 原因 -> 打ち手` まである |
| Progressive disclosure | 本文が重い or deep detail が欠落 | 分離しているが入口が弱い | `SKILL.md` は薄く、`references/` と `assets/` への導線がある |
| Fidelity | 具体例が想像だけ | 一部は具体例だが検証弱い | 実際の command / file / output に近い |

## Pass Criteria

- 合計 12/16 以上
- 次の 4 軸で 0 点を出さない
  - `Trigger clarity`
  - `First-screen success path`
  - `Decision support`
  - `Failure handling`

## Source Audit Questions

書き始める前に最低限これだけ答える。

1. この skill を読んだ人は、最終的に何を終えるのか
2. 最短成功パスは何コマンド、何ステップか
3. どの判断が branch になるか
4. どこで失敗すると痛いか
5. どの例を `assets/` にすべきか
6. どの詳細を `references/` に切るべきか

## Archetype-specific Extras

archetype ごとに最低 1 つ足りないと弱い section がある。

- Operations
  - 前提環境 table があるか
  - daily flow があるか
  - troubleshooting があるか
- Practice
  - quickstart が動く最小構成になっているか
  - decision table があるか
  - 実例か reference 導線があるか
- Meta
  - 分類規則があるか
  - 提案 / 出力テンプレートがあるか
  - `提案不要` や `対象外` の branch があるか

## Final Ship Checklist

- frontmatter の `description` を単独で読んでも trigger 条件が分かる
- 先頭 1 画面に `いつ使うか` と最短成功パスがある
- placeholder に置換ルールがある
- `references/` と `assets/` を使った場合、`SKILL.md` から直接読みに行ける
- 落とし穴が 3 件以上あるか、同等の troubleshooting がある
- 関連 skill があれば、`何のために次に読むか` が書かれている
