# Subito Price Tracker

[![Bright Data](https://img.shields.io/badge/Powered%20by-Bright%20Data-blue?style=flat-square)](https://brightdata.jp)
[![Subito Price Tracker](https://img.shields.io/badge/Subito%20Price%20Tracker-Managed%20Solution-orange?style=flat-square)](https://brightdata.jp/products/insights/price-tracker/subito)
[![Python](https://img.shields.io/badge/Python-3.9%2B-yellow?style=flat-square)](https://python.org)

[![Bright Insights Price Tracker](https://raw.githubusercontent.com/danielshashko/bright-insights-assets/main/price-tracker-hero-v2.png)](https://brightdata.jp/products/insights/price-tracker/subito)

Subito のリアルタイム価格追跡 - イタリア最大のオンラインクラシファイドプラットフォーム。開始方法は 2 通りあります: **フルマネージド**のインテリジェンスプラットフォーム、または Bright Data の AI Scraper Builder で構築する**カスタム scraper**です。

---

## Option 1: Bright Insights - AI 搭載価格追跡（推奨）

**[Bright Insights](https://brightdata.jp/products/insights/price-tracker/subito)** は、Bright Data のフルマネージドなリテールインテリジェンスプラットフォームです。scraper を構築する必要も、インフラを保守する必要もありません。構造化され、分析可能な価格データが、ダッシュボード、data feed、または BI ツールにそのまま提供されます。

**チームが Bright Insights を選ぶ理由:**
- 🚀 **セットアップ不要** - すぐに使えるダッシュボードと data feed で数分以内に利用開始
- 🤖 **AI 搭載の推奨機能** - 対話型 AI アシスタントが数百万のデータポイントを即座に実用的なインサイトへ変換
- ⚡ **リアルタイム監視** - 1 時間ごとから日次までの更新頻度と即時アラート（email、Slack、webhook）
- 🌍 **無制限のスケール** - あらゆる website、あらゆる地域、あらゆる更新頻度に対応
- 🔗 **プラグアンドプレイ統合** - AWS、GCP、Databricks、Snowflake など
- 🛡️ **フルマネージド** - Bright Data が schema 変更、site 更新、データ品質を自動で処理

**主なユースケース:**
- ✅ すべての製品カテゴリにわたって **Subito の価格を監視**
- ✅ **在庫レベルと可用性を追跡** し、リアルタイムで把握
- ✅ 注目している製品の **価格アラートを設定**
- ✅ MAP ポリシー準拠を監視し、価格違反を検出
- ✅ 競合のプロモーションと販促動向を追跡
- ✅ クリーンで正規化されたデータを、動的価格設定アルゴリズムや AI モデルに直接投入

> **月額 $250 から - [最適な見積もりを取得 →](https://brightdata.jp/products/insights/price-tracker/subito)**

---

## Option 2: 独自の Subito Scraper を構築

事前構築済みの Subito scraper API がない？問題ありません。Bright Data の **AI Scraper Builder** なら、数クリックでカスタム Subito scraper を生成できます — コーディングは不要です。

### 数分で Subito scraper を構築

**[Subito AI Scraper Builder を開く →](https://brightdata.jp/products/web-scraper/subito)**

ドメインを選択し、必要なデータ要件を記述するだけで、AI scraper builder が API を自動生成します。

1. **必要なデータを平易な英語で記述**
2. **AI が即座に scraper API を生成**
3. **API リクエストを実行してすぐに結果を取得**
4. 必要に応じて **組み込み IDE でコードを編集**

構築が完了すると、scraper には **Web Scraper ID**（`gd_xxxxxxxxxxxx`）が付与されます — 以下の Setup 手順で使用するためにコピーしてください。

### Prerequisites

- Python 3.9 以上
- [Bright Data account](https://brightdata.jp)（無料トライアルあり）
- Bright Data の **API token**（[取得方法](https://docs.brightdata.jp/general/account/account-settings#api-token)）
- Subito 用の **Web Scraper ID**（上記の構築手順で取得）

### Setup

1. **この repository を clone**

   ```bash
   git clone https://github.com/bright-jp/subito-price-tracker.git
   cd subito-price-tracker
   ```

2. **依存関係を install**

   ```bash
   pip install -r requirements.txt
   ```

3. **認証情報を設定**

   `.env.example` を `.env` にコピーし、値を入力します:

   ```bash
   cp .env.example .env
   ```

   ```env
   BRIGHTDATA_API_TOKEN=your_api_token_here
   BRIGHTDATA_DATASET_ID=your_dataset_id_here
   ```

   > **Your Web Scraper ID**
   > [AI Scraper Builder dashboard](https://brightdata.jp/products/web-scraper/subito) の Web Scraper ID を
   > `BRIGHTDATA_DATASET_ID` に貼り付けてください（形式: `gd_xxxxxxxxxxxx`）。

---

## Usage

Subito scraper の構築が完了し、Web Scraper ID が `.env` に設定されると、Python interface は同じ方法で利用できます。

### 1. URL で特定の商品を追跡

Subito の商品 URL のリストを渡して、構造化された価格データを取得します:

```python
from price_tracker import track_prices

urls = [
    "https://www.subito.it/product/sample-item-123456",
    # Add more product URLs here
]

results = track_prices(urls)
for item in results:
    print(f"{item.get('title')} - {item.get('final_price', item.get('price'))} {item.get('currency', '')}")
```

または直接実行:

```bash
python price_tracker.py
```

### 2. キーワードで商品を検索

キーワード検索に一致する商品を見つけます:

```python
from price_tracker import discover_by_keyword

results = discover_by_keyword("laptop", limit=50)
```

### 3. カテゴリ URL で商品を閲覧

Subito のカテゴリページからすべての商品を収集します:

```python
from price_tracker import discover_by_category

results = discover_by_category(
    "https://subito.it/category/example",
    limit=100,
)
```

---

## 出力フィールド

各結果レコードには次のフィールドが含まれます:

| Field | Description |
|-------|-------------|
| `url` | 商品ページ URL |
| `title` | 商品名 / タイトル |
| `brand` | ブランドまたはメーカー |
| `initial_price` | 元の価格 / 定価 |
| `final_price` | 現在の販売価格 |
| `currency` | 通貨コード（例: USD、EUR） |
| `discount` | 割引額または割引率 |
| `in_stock` | 商品が利用可能かどうか |
| `rating` | 平均星評価 |
| `reviews_count` | レビュー総数 |
| `seller_name` | 販売者名 |
| `images` | 商品画像 URL の配列 |
| `description` | 商品説明テキスト |
| `timestamp` | データ収集タイムスタンプ |

### 出力例

```json
[
  {
    "url": "https://www.subito.it/product/sample-item-123456",
    "title": "Example Product Name",
    "brand": "Example Brand",
    "initial_price": 59.99,
    "final_price": 44.99,
    "currency": "USD",
    "discount": "25%",
    "in_stock": true,
    "rating": 4.5,
    "reviews_count": 1234,
    "images": ["https://subito.it/images/product1.jpg"],
    "description": "Product description text...",
    "timestamp": "2025-01-15T10:30:00Z"
  }
]
```

---

## Advanced Options

`trigger_collection()` 関数は、データ収集を制御するためのオプションパラメータを受け付けます:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | integer | - | 返されるレコードの最大数 |
| `include_errors` | boolean | `true` | 結果に error report を含める |
| `notify` | string (URL) | - | snapshot の準備完了時に呼び出す webhook URL |
| `format` | string | `json` | 出力形式: `json`、`csv`、または `ndjson` |

オプション付きの例:

```python
from price_tracker import trigger_collection, get_results

inputs = [{"url": "https://www.subito.it/product/sample-item-123456"}]
snapshot_id = trigger_collection(inputs, limit=200, notify="https://your-webhook.com/hook")
results = get_results(snapshot_id)
```

---

## リソース

- 🌟 [Subito Price Tracker - Bright Insights (Managed)](https://brightdata.jp/products/insights/price-tracker/subito)
- 🏗️ [Build a Subito Scraper](https://brightdata.jp/products/web-scraper/subito)
- 📖 [Bright Data Web Scraper API Documentation](https://docs.brightdata.jp/scraping-automation/web-scraper-api/overview)
- 🗄️ [Web Scrapers Control Panel](https://brightdata.jp/cp/scrapers)
- 🔑 [How to get an API token](https://docs.brightdata.jp/general/account/account-settings#api-token)
- 🌐 [Bright Data Homepage](https://brightdata.jp)

---

*[Bright Data](https://brightdata.jp) を使用して構築 - 業界をリードする web data platform。*