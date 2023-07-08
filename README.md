# Webアプリケーション関連用語

## 概要
Webアプリケーションを構築する上で最低限必要な用語たちをMarkdown記法を使って記録。

## URL
- Uniform Resource Locator
- ウェブ上の特定の一意のリソース(HTML・CSS・画像)のアドレス
- リソースが存在しないもしくはすでに移動したことを示すこともある。
- 構成:<br>スキーム://オーソリティ(ドメイン:ポート番号)/パス/引数,アンカー(リソースの指定位置や時刻を表示)
~~~ 
http://example.com/path/param1/param2?query=param3
~~~

## パスパラメータ
- 一意のリソース（ユーザーIDなど）を指定する。
- ないとリソースを判別できなくなるので省略不可能。

## クエリパラメータ
- サーバーに情報を送るためにURL末尾に付け足す文字列。末尾の?の後に記述。
- なくても正常にリソースを表示できるので省略可能。
- アクセス解析用の**パッシブパラメータ**と、リソース表示に影響する**アクティブパラメータ**がある。

## HTTPメソッド
- リソースに対して実行したいアクション。

| HTTPメソッド　　 | MDN表現                             | わわわ表現              |　
|------------|-----------------------------------|--------------------|
| GET        | 指定したリソースの表現をリクエスト（データ取り込み限定）。     | ページをくれよ            |
| HEAD       | GETと同じレスポンスを、レスポンス本文なしで求める。       | ヘッダ情報だけくれ          |
| POST       | 指定したリソースに実体を送信する。                 | このデータをくれてやるよ       |
| PUT        | 対象リソースの現在の表現全体をリクエストのペイロードで置き換える。 | このデータ（ファイル）をくれてやるよ |
| PATCH      | リソースを部分的に変更する。                    | ちょっくらデータの一部を変えさせて  |
| DELETE     | 指定したリソースを削除する。                    | このデータ消しちゃって        |

参考　https://developer.mozilla.org/ja/docs/Web/HTTP/Methods　<br>
　　　https://wa3.i-3-i.info/word11405.html

## HTTPステータスコード
- 特定のHTTPリクエストが正常に完了したかどうかを示す。
1. 情報レスポンス（100番台)
2. 成功レスポンス(200番台)
3. リダイレクトメッセージ(300番台)
4. クライアントエラーレスポンス(400番台)
5. サーバーエラーレスポンス(500番台)

- 代表的なステータスコード

| コード | メッセージ                      | 意味                                     |
|-----|----------------------------|----------------------------------------|
| 200 | OK                         | リクエスト成功（GET,PUTなどメソッドにより意味が異なる）        |
| 201 | Created                    | リクエスト成功によって新たなリソースが作成された               |
| 400 | Bad Request                | 構文が無効で、サーバーがリクエストを理解できない               |
| 404 | Not Found                  | サーバーがリソースを発見できない                       |
| 500 | Internal Server Error      | サーバー側で処理方法がわからない                       |

参考　https://developer.mozilla.org/ja/docs/Web/HTTP/Status

## HTTPリクエスト
Webコンテンツの伝送を行うHTTP（Hypertext Transfer Protocol）で、クライアントからサーバへ要求を伝えるメッセージのこと。
送信してほしいファイルなどを指示する。
- リクエスト行（メソッド、URI、HTTPバージョン）
~~~
POST /search.html HTTP/1.1\r\n
~~~
- ヘッダー
- ボディ

### リクエストヘッダー
HTTPリクエストにおいて、クライアントの情報やリクエスト内容を記述する部分
- フィールド名:内容
~~~
Host: wa3.i-3-i.info\r\n
Connection: keep-alive\r\n
Content-Length: 38\r\n
Cache-Control: max-age=0\r\n
Origin: http://wa3.i-3-i.info\r\n
Upgrade-Insecure-Requests: 1\r\n
User-Agent: うんちゃら\r\n
Content-Type: application/x-www-form-urlencoded\r\n
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8\r\n
Referer: http://wa3.i-3-i.info/index.html\r\n
Accept-Encoding: gzip, deflate\r\n
Accept-Language: ja,en-US;q=0.8,en;q=0.6\r\n
~~~

### リクエストボディ
HTTPリクエストにおいて、リクエストの補足情報を記述する部分(POSTメソッドならパラメータなどを記述)
~~~
q=test&submitSearch=%E6%A4%9C%E7%B4%A2
~~~

## HTTPレスポンス
HTTPでサーバからクライアントから応答を伝えるメッセージのこと。
HTTPステータスコードや要求されたファイルの内容などで構成される。
- ステータス行（ステータスコード）
~~~ ステータス行
HTTP/1.1 200 OK\r\n
~~~

- ヘッダー
- ボディ

### レスポンスヘッダー
HTTPレスポンスにおいて、ステータスライン(ステータスコードなどが記述される部分)に書ききれないレスポンス情報が記述される部分
- フィールド名:内容
~~~ レスポンスヘッダー
Server: nginx\r\n
Date: Tue, 11 Jul 2017 09:23:07 GMT\r\n
Content-Type: text/html\r\n
Transfer-Encoding: chunked\r\n
Connection: keep-alive\r\n
~~~

### レスポンスボディ
HTTPレスポンスにおいて、ファイルの中身が記述される部分
- HTML書式
~~~ レスポンスボディ
<!DOCTYPE html>
<html>
<head>
    <title>Example Page</title>
</head>
<body>
    <h1>Welcome!</h1>
    <p>This is an example page.</p>
</body>
</html>
~~~
- XML書式
~~~ レスポンスボディ
<book>
    <title>Example Book</title>
    <author>John Smith</author>
    <year>2023</year>
</book>
~~~
- **JSON形式**

### JSON（JavaScript Object Notation）
データ交換のために設計された軽量なテキスト形式のデータ表現。
JSを元にして
~~~ 
{
  "name": "John Smith",
  "age": 30,
  "city": "New York"
}
~~~
レスポンスボディの形式はリクエストヘッダーの中で変更できる。

## Markdown記法参考記事
Markdown　入門<br>https://tech-blog.rakus.co.jp/entry/20200624/markdown <br>

Markdown記法　チートシート<br> https://qiita.com/Qiita/items/c686397e4a0f4f11683d