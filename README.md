# ビジター照合チェッカー — Vercel デプロイ手順

## フォルダ構成

```
vercel-app/
├── api/
│   └── claude.js        # Anthropic API へのプロキシ（サーバーレス関数）
├── public/
│   └── index.html       # アプリ本体
├── vercel.json          # Vercel 設定
└── README.md            # この手順書
```

---

## デプロイ手順

### 1. Anthropic APIキーを取得する

1. https://console.anthropic.com/ にアクセス
2. アカウントを作成してログイン
3. 左メニュー「API Keys」→「Create Key」
4. 生成された `sk-ant-api03-...` をコピーして保存

> 💡 APIは従量課金です。1回の照合（8名程度）で約 $0.05〜0.10 ほどかかります。

---

### 2. GitHubにアップロードする

1. https://github.com にアクセスしてログイン（アカウントがなければ無料作成）
2. 右上「+」→「New repository」
3. Repository name に `visitor-checker` など入力、「Create repository」
4. 「uploading an existing file」をクリック
5. `vercel-app` フォルダ内のファイルをすべてドラッグ＆ドロップ
   - `api/claude.js`
   - `public/index.html`
   - `vercel.json`
6. 「Commit changes」をクリック

---

### 3. Vercel にデプロイする

1. https://vercel.com にアクセスしてログイン（GitHubアカウントでOK）
2. 「Add New Project」をクリック
3. 先ほど作ったGitHubリポジトリを選択して「Import」
4. 設定はそのまま「Deploy」をクリック
5. 1〜2分でデプロイ完了、URLが発行される（例: `https://visitor-checker-xxx.vercel.app`）

---

### 4. APIキーを環境変数に設定する

1. Vercel のプロジェクトページを開く
2. 上部タブ「Settings」→ 左メニュー「Environment Variables」
3. 以下を入力して「Save」
   - **Name**: `ANTHROPIC_API_KEY`
   - **Value**: `sk-ant-api03-...`（手順1でコピーしたキー）
4. 左メニュー「Deployments」→ 最新のデプロイの「…」→「Redeploy」

---

### 5. 完了・共有

発行されたURL（例: `https://visitor-checker-xxx.vercel.app`）を
担当者に共有するだけで、ブラウザから誰でも使えます。

---

## 注意事項

- APIキーは Vercel の環境変数に保管され、利用者には見えません
- PDFはブラウザ内で処理され、サーバーにアップロードされません
- 画像化したページ画像のみが Anthropic API に送信されます
- 利用コストは Anthropic Console で確認できます
