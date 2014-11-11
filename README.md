# miCSS

**miCSS**は、[RYO NAKAE](http://brdr.jp/)がWebサイトのコーディングを行う時に使用しているCSSルールです。OOCSS、BEM、SMACSSなどから影響を受けています。読み方は自由です。


## 基本ルール

だいたい以下のルールを設けています。

* Layout、Module、State、Modifierの4つで構成される
* 全てのclassに接頭辞を付ける
* 出来るだけ全てのタグにclassを設定する
* 子要素は出来るだけ親要素の名前を引き継ぐ（BEMっぽい）
* Moduleはどこに移動しても出来るだけスタイルが崩れないようにする
* Sassなどでのネストは出来るだけ避ける
* idは使わない
* JavaScriptで参照するclassにはスタイルを当てない


## Layout, Module, State, Modifier

タグにclassを設定するする場合、必ずこの4つのどれかに分類します。

### Layout

* ヘッダー
* セクション

などの、各要素を含む大枠

### Module

* ロゴ
* ナビゲーション
* タイトル
* ボタン

などの、Layoutに内包される各要素

### State, Modifier

* ボタンのアクティブ時
* 四角いユーザーアイコンと丸いユーザーアイコン
* 1つだけ背景色が違うセクション
* トップページと下層ページでフォントサイズが違う見出し

などの、Moduleで分ける必要はないけど他と微妙に違う…みたいな状態


## 書き方

全てのclassに接頭辞を付けます。

* 気持ち見やすい
* 気持ちclassの重複が避けられる

というようなメリットがあります。

### Layout

	.l-header { ... }
	.l-section { ... }
	
などのように、Layoutは`l-`を接頭辞にします。

### Module

例えばSMACSSではModuleには接頭辞をつけません。でも別に付けてもいいよね、と思ったのでModuleにも付けます。

	.m-icon { ... }
	.m-button { ... }
	
などのように、Moduleは`m-`を接頭辞にします。

### State

文脈的に「一時的にこの状態（今はこうだけど途中で変わるかも）」というような要素に使います。

	.m-navigation.is-fixed  { ... }
	.m-alert.is-hidden  { ... }
	
などのように、`is-`を接頭辞にします。

例えばタブを切り替えた時にタブに`.is-active`を設定するようなイメージです。

### Modifier

Stateとは違い、文脈的に「他の要素と恒久的に違う」というような要素に使います。

	.m-button.m-button--large { ... }
	.l-section.l-section--fullWidth { ... }
	
などのように、MindBEMdingのModifierの書き方を参考に、classの末尾に`--modifier`というようにclass名を付けます。


## 親要素と子要素
✌(‘ω’✌ )三✌(‘ω’)✌三( ✌’ω’)✌

## Moduleの独立
✌(‘ω’✌ )三✌(‘ω’)✌三( ✌’ω’)✌

## Sassなどのネスト
✌(‘ω’✌ )三✌(‘ω’)✌三( ✌’ω’)✌

## idは使わない
✌(‘ω’✌ )三✌(‘ω’)✌三( ✌’ω’)✌


## JavaScript

要素をJavaScriptで操作する場合、

* 全くスタイルを当てていない
* 完全に独立した

上記2つのルールに沿ったclassを命名します。

### オススメ

* `js-`という接頭辞を付けたclassを追加
* `js-`という接頭辞を付けたidを追加

このどちらかにしておけば、CSSとJavaScriptが完全に独立するので良いと思います。