# coding guideline general rules

## background
仕事でHTMLやCSSを書くたびに、インデントやid、classの命名やモジュールの組み方で悩むことがあるので、おおまかな仕様を作ってしまおうと思ったのです。

とはいえこの世界は瞬く間に進歩していくもの、このガイドラインも厳守するというものではなく、新しい技術や考え方に柔軟に対応できる余地を残したものにします。

### browser
ターゲットブラウザは以下の通り

+ IE 7 以上
+ Firefox 3 以上
+ Chrome
+ Safari(mac)

ブラウザのシェア率は[StatCounter](http://gs.statcounter.com/#browser_version_partially_combined-JP-monthly-201206-201306-bar)を参考に。<br>
2013年8月23日現在ではIE6のシェアは0.52％くらいIE7でも1.06％くらい

### directory
ディレクトリの構成サンプル

    ■ site
    ├ ■ public
    │ ├ ■ css             CSS
    │ │ └ ■ sass          Sass
    │ ├ ■ images          images
    │ │ ├ ■ share/common  shared images (header, footer, sidebar)
    │ │ ├ ■ (contents)    images use in each contents
    │ │ └ ■ bnr           other images like "banners"
    │ └ ■ js              javascript
    └ index.html          home

1. css、 jsについてはリリース時にminifyする。
2. css、 jsの圧縮サービス：[YUI Compressor](http://refresh-sf.com/yui/)

### 画像
普段画像ファイルの命名には特に気を使っておりませぬが、本当はちゃんと規則を決めたほうがよいよなぁと思うので、この際ルール決め　[参考](http://www.sync-d.jp/guideline/coding/policy.html)

#### 画像ファイルの命名規則

    ○○○_×××_△△.拡張子

○○○ ＝ ページ名・部品名・ブロック名<br>
××× ＝ 画像の種類<br>
△△ ＝ 通し番号

#### 部品名
+ header
+ gnav
+ footer

#### 画像の種類
+ bg
+ btn
+ ico
+ line
+ h1,h2,h3,h4,h5,h6
+ fig

#### 通し番号
番号は2桁の数字で<br>
ただし、同一ページ内に1つしか出現しないとハッキリわかっている画像（例えばlogoとか）の場合は番号は省略してもOK。

---
update: 2013/08/23