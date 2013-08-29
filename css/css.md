# CSS guideline

## background
特にid、classの命名で時間をとられるのです。なので、そこらへんを重点的に。

### general
#### ファイルを分けるのか、まとめるのか
基本的にはどちらでもかまわない気がするけど、CSSを分割して@importすると、それだけブラウザの読み込み時間が長くなるので、まとめたほうが良いかも。Sassを使い始めてからはファイルを分割するようになったけど、あれはCSSに変換されるときには1ページにまとまるからね。

#### コメント
コメントも面倒だから基本書かないのですが…チームで作業する際には必要ですよねぇ…<br>
なので、まずはファイルの頭に目次をつけることにします。

    /* ---------------------------------------- *\
        $CONTENTS
    \* ---------------------------------------- */
    /**
     * 1.CONTENTS
     * 2.RESET
     * 3.FONT-FACE
     */

こんな風に目次をつけておくと、ファイルの中身が一目瞭然で良い感じ。<br>
それで、各セクションに

    /* ---------------------------------------- *\
        $RESET
    \* ---------------------------------------- */

    [reset style here]


    /* ---------------------------------------- *\
        $FONT-FACE
    \* ---------------------------------------- */

    [font-face style here]

みたいな感じで見出しをつけておくとよいかも。

#### CSSの記述順序
1. reset
2. エレメントのスタイル（hxとかulとかaとか）
3. デザインパターン用のスタイル（ボタンの形とか、セクションのマージンとか）
4. コンポーネント　サイト固有のCSS
5. エラー、ステータス用のCSS

#### プロパティの記述順序
アルファベット順がわかりやすくてよいのではなかろうか

    background: fuchsia;
    border:1px solid;
    -moz-border-radius: 4px;
    -webkit-border-radius: 4px;
    border-radius: 4px;
    color: black;
    height: 200px;
    text-align: center;
    text-indent: 2em;
    width: 200px;


#### module
CSSの構造を考える時は、モジュール単位で組むようにする。
例えば

    /* NG */
    .gallery{
      padding:10px;
    }
    .gallery .gallery-inner{
      margin-top:12px;
    }

    /* OK */
    .gallery{
      padding:10px;
    }
    .gallery-inner{
      margin-top:12px
    }

```
Sassで書くときも、モジュール単位に分けて記述すること。特にSassの場合ネストが便利過ぎてすぐになんでもネストしたくなってしまうので気をつける
```

### 命名規則
#### わかりやすい名前をモジュール単位でつける
命名は、そのセクションを端的に表した単語でつけるものとします。例えば

    .gallery{}
    .widget{}
    .video{}

セクションの子要素は親要素の名前を引き継いで命名します。

    .gallery__inner{}
    .widget__subset{}

使える名前としては、こんな感じ？

    block, unit, cell, item-holder, item, gallery, widget, message/note, text, login/signin, sidebar, bucket, clan, kin etc...

#### ハイフンとアンダーバー
子要素の命名の時にハイフンを使うのかアンダーバーを使うのか<br>
[csswizardryのガイドライン](https://github.com/csswizardry/CSS-Guidelines)に従って、ひとまずは下記のようなルールにします。（BEMって考え方らしい。[参考](http://bem.info/)）。<br>
ちなみに、普通に命名するときはシングルハイフンやシングルアンダーバーでええのよ。'.foo-bar'とか'.foo_bar'とか'.fooBar'とか。

    .block{}
    .block__element{}
    .block--modifier{}

+ `.block` はセクションの一番上の階層、一番上の囲みを表す
+ `.block__element` は親の階層の直接の子要素を表す
+ `.block--modifier` は子要素ではあるけども種類の違う要素を表す


```
.person{}
.person--woman{}
   .person__hand{}
   .person__hand--left{}
   .person__hand--right{}
   .person__foot{}
```

みたいな感じ。<br>
personという枠の中にpersonなんだけど種類が違う子要素としてwomanやmanがある。<br>
また、personはみなhandをもっているので、こちらはダブルアンダーバーでつなぐ。<br>
handのleftやrightは子要素だけど種類が違うのでダブルハイフンでつなぐ。

idやclass名はできるだけ短い方がいい。てか、ながい名前とか絶対忘れるし。<br>
でも、関係性をはっきりさせたい場合は長い名前はわかりやすくてよいと思う。<br>
まぁ、わかりやすさが全てです。

### OOCSSというのがありまして
[ここらへんを見るとわかりやすいかも](http://takazudo.github.io/blog/entry/2012-12-10-oocsssass.html)。<br>
[これとか](http://takazudo.github.io/presentation-oocss-sass/#/)

OOCSSは`Object Oriented CSS`の略。Nicole Sullivanという人が言い出しました。

[![Tech Talk: Nicole Sullivan - OOCSS and Preprocessors](http://img.youtube.com/vi/GhX8iPcDSsI/0.jpg)](http://www.youtube.com/watch?v=GhX8iPcDSsI)

+ [Object-Oriented CSS](http://oocss.org/)

どういうものかというと、例えば

    .room{}

    .room--kitchen{}
    .room--bedroom{}
    .room--bathroom{}

というclassを考えてみると。単純に`room`と一言でいっても、そこには色々な種類のroomが存在するわけです。台所とか、居間とか書斎とか。でも、それぞれのroomは同じような要素を共有してもいますわね。床とか屋根とか壁とか。

だったら、部屋ごとにそれぞれCSSを書くのではなくて、共用部分はまとめて書いて、差分をそれぞれの部屋のCSSに書けばいいんじゃね？という話です。

    .room{
      width: 300px;
      border-radius:4px;
      height: 45px;
    }

    .room--kitchen{
      background-color: orange;
      border:1px dotted #000;
    }
    .room--bedroom{
      background-color: green;
      border:1px dotted #aaa;
    }
    .room--bedroom{
      background-color: ivory;
      border:1px dotted #green;
    }

みたいな感じで。<br>
.room{}には共有部分のCSSを書いて、個別のCSSはそれぞれに書くのです。

    <div class="room room--kitchen"></div>
    <div class="room room--bedroom"></div>

てな風にHTMLを書きます。

これをすることで、CSSの使い回しができるようになりますね。一番最初に書いたように、モジュール単位で管理をすれば、CSSを効率よく書くことも可能です。

ちなみに、この考え方をもうちょい進めたSMACSSってのもあります。[参考](http://chroma.hatenablog.com/entry/2013/07/22/120818)<br>
あと、SMURFSってのもあるらしい。[参考](https://github.com/railslove/smurfville)  これはCSSではなくてRailなのかな

そんな感じ。
