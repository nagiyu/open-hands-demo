# open-hands-demo

OpenHands を使用して Issue から自動的に Pull Request を作成するデモリポジトリです。

## 機能

このリポジトリには、Issue が作成されたりラベルが付けられたりした際に、OpenHands AI エージェントが自動的に Pull Request を作成する GitHub Actions ワークフローが含まれています。

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

1. Issue を作成する
2. OpenHands エージェントが自動的に Issue を分析し、解決策を実装した Pull Request を作成します
3. コメントで `@openhands-agent` を使用して追加の指示を出すことも可能です

## トリガー

ワークフローは以下のイベントでトリガーされます：
- Issue が開かれた時 (`opened`)
- Issue にラベルが付けられた時 (`labeled`)
- Pull Request にラベルが付けられた時
- Issue や Pull Request にコメントが作成された時
- Pull Request レビューが提出された時