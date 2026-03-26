# homepage リンク集サイト 仕様メモ

## 現状

- `index.html` にリンクの `<ul>` を手書きしている
- GitHub Pages でホスティング予定（リポジトリ: git@github.com:paperobovino/homepage.git）

## やりたいこと

スマホのブラウザからフォームでリンクを投稿したら、サイトに自動反映されるようにしたい。

## 想定フロー

1. スマホのブラウザでフォーム画面を開く
2. タイトル・URL・パスワードを入力して送信
3. サーバーレス関数（Cloudflare Workers 等）がリクエストを受け取る
4. GitHub API 経由で `links.json` を更新・コミット
5. GitHub Pages がHTMLを自動再生成 → サイトに反映

## 構成

```
homepage/
├── index.html        # 公開ページ（links.jsonから生成）
├── links.json        # リンクデータ
├── build.js          # links.json → index.html を生成するスクリプト
└── SPEC.md           # このファイル
```

バックエンド（別リポジトリまたはCloudflare Workersダッシュボード）:
- POST エンドポイント
- パスワード認証（シンプルなトークン）
- GitHub API でlinks.jsonを読み取り・更新・コミット

## 未決事項

- [ ] バックエンドをどこにホストするか（Cloudflare Workers / Vercel / その他）
- [ ] Cloudflareアカウントの有無を確認
- [ ] フォーム画面のデザイン（最低限でよいか）
- [ ] GitHub Actions でビルドするか、手動ビルドをコミットするか
