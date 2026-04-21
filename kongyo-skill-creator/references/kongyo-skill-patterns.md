# Kongyo Skill Patterns

## まず押さえる共通項

- `description` が具体的で、`What + Use when ...` まで入っている
- body は背景説明より先に「何をすると動くか」を出す
- table を比較だけでなく分岐にも使う
- `落とし穴` が明示的で、精神論ではなく回避操作がある
- `関連` は飾りではなく、次に読むべき skill に絞られている
- 長くなる知識は `references/`、コピーしたい素材は `assets/` に逃がす

## Operations Archetype

特徴:
- 環境固有の現実に寄せる
- `前提環境` や `レイアウト早見表` のような現状把握が早い
- `日常フロー` と `トラブルシュート` が強い
- 最後に command cheat sheet を置いて再利用しやすくする

section例:
- `## 前提環境`
- `## レイアウト / 現状早見`
- `## 日常フロー`
- `## 境界条件`
- `## トラブルシュート`
- `## 参考コマンド早見`

書き方:
- path、branch、toolchain は table で固定する
- 迷いやすい `source vs dest` のような方向感覚は文章で補足する
- 事故りやすい destructive action は明示的に warning を入れる

## Practice Archetype

特徴:
- install / quickstart / principles / workflow / examples の流れが強い
- 最小成功例を先に置き、詳細は後ろに回す
- phase 分割か decision table で迷いどころを潰す
- 長い仕様は `references/` に逃がして本文を薄く保つ

section例:
- `## いつ使うか`
- `## クイックスタート`
- `## 原則`
- `## ワークフロー`
- `## Decision Table`
- `## 実例`
- `## Common Pitfalls`
- `## References`

書き方:
- クイックスタートはコピペで試せる最小構成にする
- decision table は variant 選択に使う
- 詳細仕様は `references/` に分離し、本文から読む条件を書く

## Asset-first Practice Archetype

特徴:
- 本文より先に `assets/` の価値を見せる
- `cp` して使う starter を中心に構成する
- 新規導入と既存 repo 導入で落とし穴を分ける

section例:
- `## What's in assets`
- `## Quick install`
- `## 言語 / variant 別の使い方`
- `## 既存環境への導入`
- `## トラブルシュート`

書き方:
- asset の中身を tree で見せる
- 既存環境 migration の罠を separate section にする
- `copy -> run -> verify` の流れを 3 手以内で示す

## Meta Archetype

特徴:
- 分類規則と出力契約を持つ
- `どこに書き出すべきか` を先に決める
- 提示フォーマットまで固定する

section例:
- `## いつ使うか`
- `使わない場面`
- `## 分類 / 判定`
- `## ワークフロー`
- `## 出力テンプレート`
- `## Red flags`

書き方:
- flowchart や table で判定を先に固める
- proposal は複数案を列挙し、採用待ちにする
- `重複チェック` や `提案不要` の枝も明示する

## リソース分割の基準

`kongyo` 系 skill は本文を短く保つが、情報を削ってはいない。どこに置くかを選んでいるだけ。

- `SKILL.md` に残すもの
  - 最短成功パス
  - 判断基準
  - 大きい失敗と回避策
  - 他 file を読む条件
- `references/` に逃がすもの
  - 長い CLI/API 補足
  - variant ごとの深い差分
  - rubric や kind catalog のような詳細知識
- `assets/` に置くもの
  - そのままコピーする雛形
  - 最小プロジェクト
  - 設定ファイル全文
- `scripts/` に置くもの
  - 毎回同じコードを書く処理
  - 失敗しやすく deterministic にしたい操作

## 逆に避けるもの

- 章ごとに同じ見出しを機械的に並べること
- 理屈だけで quickstart が無いこと
- `references/` に逃がしたのに入口が書かれていないこと
- 落とし穴が `気をつける` で終わること
- archetype を混ぜすぎて section 順が作業順を外すこと
