# open-hands-demo

OpenHands を使用して Issue から自動的に Pull Request を作成するデモリポジトリです。


## AI向けガイド

- ファイルの構成を見て、適切な位置にコード追加・修正を行うこと
- 読みやすいコードを書くことを意識すること
- 宣言型プログラミングを心掛けること

## 機能

このリポジトリには、Issue に `fix-me` ラベルが付与された時や、指定のマクロを含むコメントが作成された時などに、OpenHands AI エージェントが自動的に Pull Request を作成する GitHub Actions ワークフローが含まれています。

## セットアップ

ワークフローを使用するには、以下のシークレットを設定する必要があります：

### 必須シークレット
- `PAT_TOKEN`: GitHub Personal Access Token (repo, pull_request, issues 権限が必要)
- `PAT_USERNAME`: GitHub ユーザー名
- `LLM_API_KEY`: LLM API キー (Anthropic Claude など)

### オプショナルシークレット
- `LLM_BASE_URL`: カスタム LLM ベース URL

### オプショナル変数
- `OPENHANDS_MACRO`: トリガーマクロ (デフォルト: `@openhands-agent`)
- `OPENHANDS_MAX_ITER`: 最大イテレーション数 (デフォルト: 50)
- `OPENHANDS_BASE_CONTAINER_IMAGE`: ベースコンテナイメージ
- `LLM_MODEL`: 使用するLLMモデル (デフォルト: `anthropic/claude-sonnet-4-20250514`)
- `TARGET_BRANCH`: ターゲットブランチ (デフォルト: `main`)
- `TARGET_RUNNER`: ランナー指定

## 使い方

1. Issue を作成し、`fix-me` ラベルを付与する
2. `fix-me` ラベルが付与された Issue に対して、OpenHands エージェントが自動的に Issue を分析し、解決策を実装した Pull Request を作成します
3. Issue、Pull Request、Pull Request レビューコメントに「@openhands-agent」(または `OPENHANDS_MACRO` で指定したマクロ) を含むコメントを追加することで、追加の指示を出すことも可能です

## トリガー

ワークフローは以下のイベントでトリガーされます：
- Issue に `fix-me` ラベルが付与された時
- Pull Request がアサインされた時
- Issue、Pull Request、Pull Request レビューコメントに「@openhands-agent」(または `OPENHANDS_MACRO` で指定したマクロ) を含むコメントが作成された時

※ コメントによるトリガーは、コメント本文にマクロが含まれている場合のみ発火します。
