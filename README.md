# cc-tips

Claude Code の活用 Tips、設定例、ベストプラクティスを集約したナレッジベースリポジトリ

## 📖 概要

このリポジトリは、Claude Code をより効果的に活用するための Tips やノウハウを体系的にまとめたものです。

**想定読者:**
- Claude Code を使い始めたばかりのユーザー
- Claude Code の機能をもっと活用したい方
- チームで Claude Code のベストプラクティスを共有したい方

**提供する価値:**
- すぐに使えるプラグインの紹介
- 設定の最適化方法
- 効率的なワークフローの構築方法
- よくある課題の解決策

## 📚 Tips 一覧

| Tips | 概要 | カテゴリ |
|------|------|---------|
| [推奨プラグイン](tips/recommend-plugin.md) | code-simplifier, code-review などの便利なプラグインの紹介とトレードオフ | プラグイン |
| [開発支援コマンド](tips/custom-slash-commands.md) | /create_pr, /git_sync, deep-dive など開発フローを効率化するコマンド・プラグイン | ワークフロー |
| [Skills 整理方法](tips/skills-organization.md) | Skills に何を置くべきかの判断基準（再利用可能性で分類） | 設計思想 |
| [CLAUDE.md設定](tips/claude-md-configuration.md) | グローバル設定と@インポート方式のベストプラクティス | 設定 |
| [ccusage設定](tips/ccusage-setup.md) | Claude Codeのトークン使用量とコスト追跡の設定方法 | 設定 |

## 🚀 クイックスタート

### 推奨プラグインのインストール

```bash
# code-simplifier - コードの明確性・保守性向上
/plugin marketplace update claude-plugins-official
/plugin install code-simplifier

# code-review - PRレビュー自動化
/plugin marketplace add anthropics/claude-code
/plugin install code-review
```

### Skills の整理

**判断基準: 再利用可能かどうか**

- ✅ **Skills に置く**: チェックリスト、命名規則、設計パターン（再利用可能）
- ❌ **docs/ に置く**: プロジェクト固有の決定、一時的なログ（コンテキスト固有）

詳細は [Skills 整理方法](tips/skills-organization.md) を参照

## 📁 リポジトリ構造

```
cc-tips/
├── tips/               # カテゴリ別 Tips ドキュメント
│   ├── recommend-plugin.md
│   ├── custom-slash-commands.md
│   ├── skills-organization.md
│   ├── claude-md-configuration.md
│   └── ccusage-setup.md
├── examples/           # 設定ファイルやスクリプトの実例（予定）
├── templates/          # 再利用可能なテンプレート（予定）
└── docs/               # 詳細ドキュメント（予定）
```

## 🤝 コントリビューション

Tips の追加や改善を歓迎します！

### Tips 追加の流れ

1. **Issue を作成** - 追加したい Tips の概要を記載
2. **ブランチを作成** - `feature/add-tips-xxx` 形式
3. **Tips を作成** - `tips/` ディレクトリに Markdown ファイルを追加
4. **PR を作成** - レビュー後にマージ

### フォーマットガイドライン

- Tips は具体的で再現可能な形式で記述
- 設定例には使用場面とトレードオフを明記
- Markdown の一貫したフォーマットを維持

**Tips テンプレート:**

```markdown
# Tips タイトル

簡潔な説明文

## 概要
- 目的
- 対象読者

## 使い方
- 手順1
- 手順2

## トレードオフ
- ✅ メリット:
- ⚠️ デメリット:

## 参考リンク
```

## 🔗 関連リンク

- [Claude Code 公式サイト](https://code.claude.com/)
- [Claude Code ドキュメント](https://code.claude.com/docs)
- [Claude Plugins 公式リポジトリ](https://github.com/anthropics/claude-plugins-official)

## 📄 ライセンス

このリポジトリの内容は、学習・共有を目的としています。
