# ccusage 設定ガイド

Claude Code のトークン使用量とコストを追跡する CLI ツール。

**公式:** https://github.com/ryoppippi/ccusage

---

## クイックスタート

### 1. Bun のインストール（ステータスライン用）

```bash
curl -fsSL https://bun.sh/install | bash
```

### 2. ステータスライン設定

`~/.claude/settings.json` に追加:

```json
{
  "statusLine": {
    "type": "command",
    "command": "bun x ccusage statusline",
    "padding": 0
  }
}
```

### 3. Claude Code を再起動

ステータスラインにコスト情報が表示されます。

---

## ステータスライン表示パターン

### パターン1: コストのみ（デフォルト）

```json
{
  "statusLine": {
    "type": "command",
    "command": "bun x ccusage statusline",
    "padding": 0
  }
}
```

表示: `💰 $0.42 (2.1K tokens)`

### パターン2: ディレクトリ名 + コスト

```json
{
  "statusLine": {
    "type": "command",
    "command": "echo \"$(basename $(pwd)) | $(bun x ccusage statusline)\"",
    "padding": 0
  }
}
```

表示: `cc-tips | 💰 $0.42 (2.1K tokens)`

### パターン3: 相対パス + コスト

```json
{
  "statusLine": {
    "type": "command",
    "command": "echo \"$(pwd | sed \"s|^$HOME|~|\") | $(bun x ccusage statusline)\"",
    "padding": 0
  }
}
```

表示: `~/Work/git/.../cc-tips | 💰 $0.42 (2.1K tokens)`

### パターン4: Git ブランチ + コスト（推奨）

```json
{
  "statusLine": {
    "type": "command",
    "command": "echo \"$(pwd | sed \"s|^$HOME|~|\") [$(git branch --show-current 2>/dev/null || echo '-')] | $(bun x ccusage statusline)\"",
    "padding": 0
  }
}
```

表示: `~/Work/.../cc-tips [main] | 💰 $0.42 (2.1K tokens)`

**トレードオフ:**
- Git ブランチ表示は実行時間が若干増加
- パス表示は画面幅を消費

---

## コマンドリファレンス

### 基本コマンド

```bash
npx ccusage daily      # 日次レポート
npx ccusage monthly    # 月次レポート
npx ccusage session    # セッション別
npx ccusage blocks     # 5時間ブロック（課金ウィンドウ）
```

### よく使うオプション

```bash
--breakdown            # モデル別コスト内訳
--since 20250525       # 開始日
--until 20250530       # 終了日
--locale ja-JP         # 日本語表示
--compact              # コンパクト表示
--json                 # JSON 出力
--timezone Asia/Tokyo  # タイムゾーン指定
```

### 実用例

```bash
# エイリアス設定（~/.zshrc）
alias cc-cost='npx ccusage@latest daily --locale ja-JP'

# 月次コスト集計
npx ccusage monthly --breakdown --locale ja-JP

# 期間指定でJSON出力
npx ccusage session --since 20250101 --until 20250131 --json > cost.json
```

---

## トラブルシューティング

| 問題 | 原因 | 解決策 |
|-----|------|-------|
| ステータスライン非表示 | Bun 未インストール | `curl -fsSL https://bun.sh/install \| bash` |
| データなし | ログファイル未生成 | Claude Code を使用後に再確認 |
| 動作が遅い | ログ蓄積 | `--since` で期間を絞る |

ログファイルの場所: `~/.claude/usage.jsonl`

---

## 参考リンク

- [ccusage GitHub](https://github.com/ryoppippi/ccusage)
- [ccusage ドキュメント](https://ccusage.com/)
- [Bun 公式](https://bun.sh/)
