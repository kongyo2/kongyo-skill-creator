# kongyo-skill-creator

`kongyo` 式の skill を作るための Claude Code プラグインです。知識の羅列ではなく「その場で動ける運用メモ」に仕上げることを目的とした skill `kongyo-skill-creator` を収録しています。

新規 skill の作成、説明中心の既存 skill を実行可能なランブックに書き直したい場合、チーム内の skill を同じ書き味に揃えたい場合に呼び出してください。

## 収録スキル

| Skill | 用途 |
|---|---|
| `kongyo-skill-creator` | trigger 明確化、first-screen quickstart、decision table、コピペ雛形、落とし穴と troubleshooting を備えた `SKILL.md` / `references/` / `assets/` へ整形する |

skill の詳細は [`kongyo-skill-creator/SKILL.md`](./kongyo-skill-creator/SKILL.md) を参照してください。3 つの archetype 分類や review checklist は [`kongyo-skill-creator/references/`](./kongyo-skill-creator/references) にあります。

## インストール

### Claude Code のマーケットプレイスから導入

Claude Code は [プラグインマーケットプレイス経由でプラグインを配布](https://code.claude.com/docs/en/discover-plugins.md) できます。本リポジトリは `.claude-plugin/marketplace.json` を含むため、そのままマーケットプレイスとして追加できます。

Claude Code を起動して次のコマンドを実行してください。

```shell
/plugin marketplace add kongyo2/kongyo-skill-creator
/plugin install kongyo-skill-creator@kongyo-skill-creator
```

対話的に選びたい場合は、マーケットプレイス追加後に `/plugin` を開き、**Discover** タブから `kongyo-skill-creator` を選択してインストールできます。インストール後に skill を反映するには `/reload-plugins` を実行してください。

skill の一般的な仕組み（`SKILL.md` の場所、`name` / `description` frontmatter、自動起動の流れなど）は [Skills のドキュメント](https://code.claude.com/docs/en/skills.md) を参照してください。

### vercel-labs/skills の `npx skills` CLI から導入

[vercel-labs/skills](https://github.com/vercel-labs/skills) が提供する `npx skills` CLI を使うと、Claude Code に限らず OpenCode / Codex / Cursor など多数のエージェントに同じ skill を配ることができます。

```shell
# GitHub shorthand（推奨）
npx skills add kongyo2/kongyo-skill-creator

# 完全な GitHub URL を指定する場合
npx skills add https://github.com/kongyo2/kongyo-skill-creator
```

よく使うオプション:

| オプション | 用途 |
|---|---|
| `-g, --global` | プロジェクトではなくユーザーディレクトリ（`~/.claude/skills/` など）にインストール |
| `-a, --agent <agents...>` | インストール先のエージェントを指定（例: `-a claude-code`） |
| `-s, --skill <skills...>` | インストールする skill を名前で指定 |
| `-y, --yes` | 確認プロンプトをスキップ（CI 向け） |
| `--copy` | シンボリックリンクではなくコピーで配置 |

例: Claude Code の user scope にのみ非対話で入れる。

```shell
npx skills add kongyo2/kongyo-skill-creator --skill kongyo-skill-creator -g -a claude-code -y
```

更新・削除・一覧:

```shell
npx skills list                                    # 導入済みの skill を一覧
npx skills update kongyo-skill-creator             # 最新に更新
npx skills remove kongyo-skill-creator             # 削除
```

Claude Code 以外のエージェントの保存先や対応状況は vercel-labs/skills の README にある Supported Agents 表を参照してください。

### 手動でクローンして配置する

Claude Code 単体で運用するなら、リポジトリをクローンして skill ディレクトリをコピーするだけでも動きます。

```shell
git clone https://github.com/kongyo2/kongyo-skill-creator.git
cp -r kongyo-skill-creator/kongyo-skill-creator ~/.claude/skills/
```

プロジェクト単位で共有する場合は `.claude/skills/` 配下に置いてください。

## 使い方

インストール後、skill は description の trigger に該当する作業をすると自動的に読み込まれます。明示的に呼び出したいときは会話で名前を挙げるだけで十分です。

```
kongyo-skill-creator を使って、この skill をレビューしつつ kongyo 流に書き直して。
```

典型的な出番:

- 新しく skill を書き始める前の骨組み確認
- 既存 skill の `description` が曖昧で trigger しづらいとき
- 説明ばかりで quickstart が埋もれている skill を作業順に並べ替えたいとき
- チーム内の複数 skill を同じ archetype パターンに揃えたいとき

## 参考

- [Claude Code: Discover and install plugins](https://code.claude.com/docs/en/discover-plugins.md)
- [Claude Code: Skills](https://code.claude.com/docs/en/skills.md)
- [anthropics/skills](https://github.com/anthropics/skills) — 公式 skill 例と template
- [cloudflare/skills](https://github.com/cloudflare/skills) — マーケットプレイス配布と `npx skills` 導入の実例
- [vercel-labs/skills](https://github.com/vercel-labs/skills) — 複数エージェント対応の skill CLI

## ライセンス

[MIT](./LICENSE)
