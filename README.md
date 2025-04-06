# NewsAPI-
感情分析のニュースを収集するためのコードです。
import requests

# 自分のAPIキー
API_KEY = ''

# ニュースを取得するURL
url = "https://newsapi.org/v2/everything"

# リクエスト送信するためのパラメータ
params = {
    'q': '',  # 検索ワード　任意のワードをここに入れる
    'apiKey':'' # 自分のAPIキー
}

# ニュースデータを取得
response = requests.get(url, params=params)

# レスポンスのステータスコードとJSONデータを確認
if response.status_code == 200:
    print("ニュースデータ取得成功！")
else:
    print("ニュースデータの取得に失敗しました。")
    print(f"ステータスコード: {response.status_code}")
    exit()

# レスポンスのJSONデータを取得
data = response.json()

# 記事が取得できた場合にニュースをファイルに書き込む
if data.get('articles'):
    with open("/Users/ui/Desktop/news_data.txt", "w", encoding="utf-8") as file:
        for article in data['articles']:
            title = article.get('title', 'タイトルなし')  # 記事のタイトル
            description = article.get('description', '説明なし')  # 記事の説明
            url = article.get('url', 'URLなし')  # 記事のURL
            published_at = article.get('publishedAt', '公開日なし')  # 記事の公開日

            file.write(f"タイトル: {title}\n")
            file.write(f"説明: {description}\n")
            file.write(f"公開日: {published_at}\n")
            file.write(f"URL: {url}\n")
            file.write("\n" + "-"*50 + "\n\n")
else:
    print("記事が取得できませんでした。")
