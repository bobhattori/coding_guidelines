# html guideline to the galaxy...
version: 0.01

## background
言わずもがなではありますが、HTMLをできる限りシンプルで美しく、かつ効率よく書くためにルールで決められる部分は決めてしまえと思ったわけでして。<br>
参考は[Google style guide](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml)

### protocol
Google先生は、絶対パスを書く際、頭の「http:」を抜きなさいと言っているのですが（[ここで](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml#Protocol)）、実際にやってみるとどうもうまくいかないようなので（ローカルだからか？）、リンクをフルパスで記述するときは従来通り「http:」から書くこととします。

### format
#### indentation
インデントは半角スペース'2つ分'で。タブとスペースが混在しないように気をつける

```
note
とはいえ、mixuteやその他のフロントエンド用プラットフォームでテンプレートを使って作業する場合、HTMLにインデントをつけると煩雑になってしまうのです。インデントをつけた方が間違いなく見やすいので、とりあえずはテンプレートを使うときは気をつける、しかないのか…
```

### meta
#### encoding
エンコードは特別なことがない限り BOMなしUTF-8で

#### comments
コメントは必要とされる箇所に書く

### HTML style rules
#### Document type
特別な場合がない限りHTML5で書く。

    <!doctype html>

#### semantics
目的に応じてHTMLを記述すること<br>
見出しならばhx要素、段落ならばp要素、アンカーはa要素など。

#### multimedia fallback
'img'や'videos'などには原則'alt="hoge"'をつける。矢印画像などの賑やかしについては省略してもかまわない。


### HTML Format
#### head

##### title
特に指定がない限りは

    ページ名｜会社名（サイト名）
    ページ名：カテゴリー名｜会社名（サイト名）

##### meta
###### description/keyword
原稿に記載がない場合は空で

    <meta name="description" content="">
    <meta name='keywords' content="">