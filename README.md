# miCSS

**miCSS**は、[RYO NAKAE](http://brdr.jp/)がWebサイトのコーディングを行う時に使用しているCSSルールです。  
OOCSS、BEM、SMACSS、知人友人などから影響を受けています。ちなみに読み方は自由です。


## 基本ルール

だいたい以下のルールを設けています。

* HTMLは**Layout、Module、State、Modifier**の4つで構成され、それぞれ接頭辞をつける
* JavaScriptで操作するclassには上記とは別の接頭辞をつけ、スタイルを当てない
* idは使わない
* 出来るだけ全てのタグにclassを設定する
* 出来るだけ子要素は親要素の名前を引き継ぐ（BEMっぽく）
* 出来るだけModuleは独立させる
* 出来るだけSassなどでのネストは避ける
* あまりルールにこだわりすぎず、無理な時は無理と諦める寛容な心を持つ


## Layout, Module, State, Modifier

タグにclassを設定する場合、必ずこの4つのどれかに分類します。

### 接頭辞をつける

全てのclassに接頭辞をつけます。

* 気持ち見やすい
* 気持ちclassの重複が避けられる

というようなメリットがあります。

### Layout

* ヘッダー
* セクション

などの、各要素を含む大枠

	.l-header { ... }
	.l-section { ... }
	
などのように、Layoutは`l-`を接頭辞にします。

### Module

* ロゴ
* ナビゲーション
* タイトル
* ボタン

などの、Layoutに内包される各要素

例えばSMACSSではModuleには接頭辞をつけません。でも別に付けてもいいよね、と思ったのでModuleにも付けます。

	.m-icon { ... }
	.m-button { ... }
	
などのように、Moduleは`m-`を接頭辞にします。

### State, Modifier

* ボタンのアクティブ時
* 四角いユーザーアイコンと丸いユーザーアイコン
* 1つだけ背景色が違うセクション
* トップページと下層ページでフォントサイズが違う見出し

などの、「わざわざModuleで分ける必要はないけど他と微妙に違う…」というような要素

#### State

文脈的に「一時的にこの状態（今はこうだけど途中で変わるかも）」というような要素に使います。

	.m-navigation.is-fixed  { ... }
	.m-alert.is-hidden  { ... }
	
などのように、`is-`を接頭辞にします。

例えば、タブを切り替えた時にタブに`.is-active`を設定するようなイメージです。

### Modifier

Stateとは違い、文脈的に「他の要素と恒久的に違う」というような要素に使います。

	.m-button.m-button--large { ... }
	.l-section.l-section--fullWidth { ... }
	
などのように、MindBEMdingのModifierの書き方を参考に、classの末尾に`--modifier`というようにclass名を付けます。

例えば、「特定のセクションが色だけ違うけど、`is-hoge`と命名するのはしっくりこない…」という微妙な気持ちの時に使います。


## JavaScript用の接頭辞

要素をJavaScriptで操作する場合、

* 全くスタイルを当てていない
* 完全に独立した

上記2つのルールに沿ったclassを命名します。`js-`というのがオススメです。

* `js-`という接頭辞を付けたclassを追加
* `js-`という接頭辞を付けたidを追加

このどちらかにしておけば、CSSとJavaScriptが完全に独立するので良いと思います。


## idは使わない

idは強力すぎるので使いません。CSSで要素を指定する場合は全てclassで行います。

JavaScriptで要素を探す場合はidが便利なので使っても良いです。


## 子要素は親要素の名前を引き継ぐ

子要素は**出来るだけ**親要素のclass名を引き継ぐようにします。

    <div class="entryList">
      <div class="entryList-item">
        <h1 class="entryList-item-title">エントリータイトル</h1>
        <p class="entryList-item-text">エントリー本文</p>
      </div>
    </div>

このように子要素は親要素の名前を引き継ぐようにすると、class名の重複が防げます。Sassなどでネストする必要もなくなるので、良い感じのCSSが書けます。  
`.entryList-item`のように、親要素と子要素はハイフンで繋ぎます。

例えば「Entry Title Block」のように要素の名前が長い場合、`.entryTitleBlock`のように、

* 頭文字は小文字
* 2つ目以降の単語の頭文字を大文字
* ハイフンなしで連結

して書くようにします。こうすると親要素と子要素をハイフンで繋ぐことが出来ます。

僕の中のゴーストが「Modifierと見間違える」とささやくので、今後もしかしたらアンダースコアで繋ぐかも知れません。


## Moduleの独立

Moduleは**出来るだけ**独立させるようにします。

    ✌(‘ω’✌ )三✌(‘ω’)✌三( ✌’ω’)✌


## Sassなどでのネスト

SassなどのメタCSS言語でのネスト（入れ子）は**出来るだけ**避けるようにします。

    ✌(‘ω’✌ )三✌(‘ω’)✌三( ✌’ω’)✌
    
    
## ルールにこだわりすぎない

あまりルールにこだわりすぎると例外が発生した時に詰むので、その時は潔く諦める寛容な精神が必要です。

[Rules of Three](http://qiita.com/usako/items/de252b7f7e43e5161fcb#2-2)という素晴らしい言葉があります。

例えばModuleを作る時なども、

* まずはひたすら親要素にネストして組む
* 別の箇所でまた同じ要素が出てきても、まだ我慢して親要素にネストする
* 3回同じ要素が出てきたら、初めてそこで子要素をModule化する（前2箇所も書き直す）

というようにすることで、いちいち「ここはModuleになるかな…いやどうかな…」などと悩まずに済むようになります。


***


## 最近の悩み

* Grid Systemとどうやって共存させるか
* 未だに「これLayoutかModuleどっちなん」と悩む場合がある
* `div.image img`や`h1.title a`のようなimgやaにもclassを設定すべきか（完全に全ての要素にclassを設定すべきか）
* Module単位でSassファイル分けるとMiddlemanのLiveReloadがLiveRelaodにならない