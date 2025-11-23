# README

このREADMEは、アプリケーションを起動して実行するために必要な手順を文書化するものです。

カバーすべき事項：

* Rubyのバージョン

* システム依存関係

* 設定

* データベースの作成

* データベースの初期化

* テストスイートの実行方法

* サービス（ジョブキュー、キャッシュサーバー、検索エンジンなど）

* デプロイ手順

# 練習日程調整アプリ

バンドの練習日程を効率的に調整するためのWebアプリケーションです。

## 機能

- **複数バンド管理**: 複数のバンドを作成し、それぞれ独立して管理できます
- **メンバー管理**: メンバーを登録し、複数のバンドに所属させることができます
- **空き時間入力**: 週ごとに各メンバーの空き時間を曜日・時間帯で登録できます
- **可視化**: メンバー全員の空き時間が重なっている時間帯を自動的に検出し、強調表示します
- **スマホ対応**: モバイルデバイスからの操作を考慮したレスポンシブデザイン

## 技術スタック

- **バックエンド**: Ruby on Rails 8.0.4
- **Ruby**: 3.4.7
- **フロントエンド**: Bootstrap 5.3
- **データベース**: PostgreSQL 18.1
- **コンテナ**: Docker Compose

## 環境構築

### 前提条件

- Docker Desktop for Mac がインストールされていること
- Docker Compose がインストールされていること

### セットアップ手順

1. リポジトリをクローン

```bash
git clone <repository-url>
cd practice_planner
```

2. Docker Composeでコンテナを起動

```bash
docker compose up -d
```

3. データベースを作成

```bash
docker compose exec web bin/rails db:create
docker compose exec web bin/rails db:migrate
```

4. ブラウザでアクセス

```
http://localhost:3000
```

### よく使うコマンド

```bash
# コンテナの起動
docker compose up -d

# コンテナの停止
docker compose down

# ログの確認
docker compose logs -f web

# Railsコンソールを起動
docker compose exec web bin/rails console

# テストの実行
docker compose exec web bin/rails test

# Gemのインストール（Gemfileを変更した場合）
docker compose build web
docker compose up -d

# データベースのリセット
docker compose exec web bin/rails db:reset
```

## 開発

### ローカル開発（Docker不使用）

ローカルでPostgreSQLを起動している場合は、以下の環境変数を設定してください：

```bash
export DATABASE_HOST=localhost
export DATABASE_USER=postgres
export DATABASE_PASSWORD=your_password
```

その後、通常通りRailsを起動：

```bash
bin/rails server
```

## デプロイ

本番環境へのデプロイにはKamalを使用します。詳細は`config/deploy.yml`を参照してください。
