# open-hands-demo

OpenHands を使用して Issue から自動的に Pull Request を作成するデモリポジトリです。

## 機能

このリポジトリには、OpenHands AI エージェントが自動的に Issue を分析し、Pull Request を作成する GitHub Actions ワークフローが含まれています。

GitHub Actions のワークフローは [All-Hands-AI/OpenHands](https://github.com/All-Hands-AI/OpenHands) の reusable workflow を呼び出す形で構成されています。
**2025年6月現在の OpenHands GitHub Actions の使い方に合わせて README を最新化しています。**


## セットアップ

ワークフローを使用するには、以下のシークレットを設定する必要があります：

### 必須シークレット
- `PAT_TOKEN`: GitHub Personal Access Token (repo, pull_request, issues 権限が必要)
- `PAT_USERNAME`: GitHub ユーザー名
- `LLM_API_KEY`: LLM API キー (Anthropic Claude など)

### オプショナルシークレット
- `LLM_BASE_URL`: カスタム LLM ベース URL

### オプショナル変数
- `OPENHANDS_MACRO`: トリガーマクロ（デフォルト: `@openhands-agent`）
- `OPENHANDS_MAX_ITER`: 最大イテレーション数（デフォルト: 50）
- `OPENHANDS_BASE_CONTAINER_IMAGE`: ベースコンテナイメージ
- `LLM_MODEL`: 使用する LLM モデル（デフォルト: `anthropic/claude-sonnet-4-20250514`）
- `TARGET_BRANCH`: ターゲットブランチ（デフォルト: `main`）
- `TARGET_RUNNER`: 実行ランナー（必要に応じて指定）

## 使い方

1. Issue を作成する
2. 必要に応じて `fix-me` ラベルを手動で付与する
3. OpenHands エージェントが自動的に Issue を分析し、解決策を実装した Pull Request を作成します
4. Issue や Pull Request のコメントで `@openhands-agent`（または `OPENHANDS_MACRO` で指定したマクロ）を使って追加指示を出すことも可能です

## トリガー

ワークフローは以下のイベントでトリガーされます：
- Issue に `fix-me` ラベルが付与された時
- Pull Request がアサインされた時
- Issue や Pull Request にコメントが作成され、`@openhands-agent`（または `OPENHANDS_MACRO` で指定したマクロ）が含まれている時
- Pull Request レビューコメントに `@openhands-agent`（または `OPENHANDS_MACRO` で指定したマクロ）が含まれている時

> 以前の「Issue 作成時に自動で `fix-me` ラベルを付与」や「PR にラベルが付いた時」などの挙動は、現在のワークフローでは行われません。必要に応じてラベル付与やマクロコメントを手動で行ってください。
