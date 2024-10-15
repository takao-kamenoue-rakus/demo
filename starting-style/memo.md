# @staring-style

## @staring-styleとは
- [MDN](https://developer.mozilla.org/ja/docs/Web/CSS/@starting-style)

> @starting-style は CSS のアットルールで、トランジションさせる要素に設定されるプロパティ群の開始値を定義するために使用します。これらのプロパティは、最初に要素のスタイルが更新されたとき、つまり要素が前回読み込まれたページに最初に表示されたときに設定されるものです。

- 初期表示時にトランジションさせるプロパティを設定
  - `@starting-styleのプロパティ群 -> 通常のプロパティ群` へとトランジションする
- 初期表示に限った話ではなく、動的に状態を変化させたい時でも使用
  - `display:none -> display: block`

## display の transition

下記のCSSはtransitionがきかない

```css
.box {
  display: none;
}
.box:hover {
  display: block;
  transition: 0.7s;
}
```

理由はdisplayは離散プロパティではないから。

## 離散プロパティとは

CSSのプロパティには補完可能なプロパティと離散プロパティが定義されている。
displayのAnimation Typeはnot animatableなので、アニメーションがきかない。

- [Web Animations 仕様](https://www.w3.org/TR/web-animations/#animation-type)
- [display 仕様](https://drafts.csswg.org/css-display/#the-display-properties)

## transition-behaviorプロパティ

transition-behaviorプロパティにallow-discreteを指定することで、アニメーションが有効となる。

- [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/transition-behavior)

## 離散アニメーションの挙動

- 2 つの値の間をアニメーションの 50% で切り替える
- display: none と content-visibility: hiddenだけ例外。
  - display を none -> block に切り替わる時、即座に0 -> 100%となる
  - display を block -> none に切り替わる時、値は完全に none に切り替わった時に0%になる