# 推奨プラグイン

Claude Code の便利な公式プラグインの紹介。

## 概要

| プラグイン | 目的 | 呼び出し方 | インストール元 |
|-----------|------|-----------|---------------|
| code-simplifier | コードの明確性・保守性向上 | 自動 / 手動フレーズ | claude-plugins-official |
| code-review | PRレビュー自動化 | `/code-review` コマンド | anthropics/claude-code |

## code-simplifier

コードの明確性・一貫性・保守性を向上させるエージェント。機能を保持しながら、実装方法のみを改善します。

**主な責務:**
- 機能保持（動作は変えず実装方法のみ改善）
- プロジェクト基準の適用（CLAUDE.mdに従った実装）
- 可読性向上（ネスト削減、冗長コード排除）
- バランス維持（過度な単純化を回避）

**使い方:**
- **自動発動**: 最近修正されたコードに対して自動的に分析
- **手動呼び出し**: "Simplify this code", "Make this clearer", "Refine this implementation"
- **エージェント呼び出し**: @agent-code-simplifier:code-simplifier
- **範囲**: 指示がない限り広い範囲は対象外
- **モデル**: Opus を使用して詳細な分析を実施

**トレードオフ:**
- ✅ **メリット**: コード品質・可読性が向上、保守性の改善、プロジェクト基準への自動準拠
- ⚠️ **デメリット**: Opusモデル使用によりAPI利用コストが高い、自動発動時に意図しない変更が提案される可能性、詳細分析のため実行時間が長め

**インストール:**
```bash
/plugin marketplace update claude-plugins-official
/plugin install code-simplifier
```

## code-review

PRレビューを自動化するプラグイン。複数エージェントを並行実行し、信頼度スコアリングで誤検知をフィルタリングします。

**5つの並行エージェント:**
1. CLAUDE.mdコンプライアンス監査（2つ）
2. バグ検出
3. 履歴コンテキスト分析（git blame）
4. コードコメント分析

**信頼度スコアリング:**
- 0-100スケールで各指摘をスコアリング
- デフォルト閾値80でフィルタリング（設定変更可能）

**使い方:**
- `/code-review` - ローカル実行（ターミナルに出力）
- `/code-review --comment` - PRコメントとして投稿
- 自動スキップ: クローズ済みPR、ドラフトPR、既レビュー済みPR

**トレードオフ:**
- ✅ **メリット**: 包括的な多角的レビュー、信頼度スコアリングで誤検知を削減、CLAUDE.md準拠チェック
- ⚠️ **デメリット**: 5エージェント並行実行のため時間がかかる（大規模PRでは数分）、閾値80では重要な指摘を見逃す可能性、閾値を下げると誤検知が増加

**インストール:**
```bash
/plugin marketplace add anthropics/claude-code
/plugin install code-review
```

## 使用例

### code-simplifier の活用

```bash
# コミット前にコードを簡潔化
$ git diff HEAD
# Claude Codeで確認
"この変更をシンプルにできる?"
```

### code-review の活用

```bash
# PR作成後にレビュー実行
$ gh pr create --title "Add feature X"
$ /code-review --comment
# → PRにレビューコメントが自動投稿される
```

<!-- TODO(human): code-simplifier で劇的に改善したコード例、code-review で見つかった重大なバグの事例、プラグインのカスタマイズ設定（信頼度閾値など）があれば追記してください -->

## 参考リンク

- [claude-plugins-official/code-simplifier](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/code-simplifier)
- [claude-plugins-official/code-review](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/code-review)
- [Claude Code Plugins 公式ドキュメント](https://code.claude.com/docs/en/plugins)
