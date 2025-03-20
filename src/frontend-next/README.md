This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.js`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.

## Docker対応

Next.jsアプリケーションをDocker化するための手順は以下のとおりです：

### ローカルでのDockerイメージのビルドと実行

```bash
# Makefileを使用したビルド
make dockerhub-build

# または直接ビルド
docker build -t kurosawakuro/frontend-nextjs-3000:latest .

# コンテナを実行（ポート3000をホストの3000にマッピング）
docker run -p 3000:3000 kurosawakuro/frontend-nextjs-3000:latest
```

### Docker Hubへのプッシュ

```bash
# Makefileを使用したデプロイ
make dockerhub-deploy

# または個別のステップで実行
make dockerhub-login
make dockerhub-build
make dockerhub-push
```

### Terraform設定の更新

フロントエンドアプリケーションをFargateで実行するには、以下の手順でTerraform設定を更新してください：

1. Terraformの設定ファイルでイメージを指定
2. ECSタスク定義でフロントエンドコンテナを追加
3. ALBリスナールールを更新してフロントエンドへのトラフィックを設定

```terraform
# フロントエンドコンテナの設定例
{
  name      = "frontend-next-container",
  image     = "kurosawakuro/frontend-nextjs-3000:latest",
  essential = true,
  portMappings = [
    {
      containerPort = 3000,
      hostPort      = 3000,
      protocol      = "tcp"
    }
  ]
}
```
