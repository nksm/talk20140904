

# 概要 #

Web Componentsは、Web の UI をコンポーネント化するための仕様。
現在、W3C で仕様の策定が進んでいる。

---

## なぜ、今Web Components？

---

## PC版Decolog のポップアップのマークアップ ##

```html
<div class="pulldown">
    <div class="pulldown-label">
        <button>
            <span class="pulldown-label-text">デフォルト</span>
            <span class="pulldown-btn"><i class="pulldown-btn-icon icon icon-triangle"></i></span>
        </button>
    </div>
    <div class="pulldown-menu">
        <ul class="pulldown-items">
            <li class="pulldown-item"><button>デフォルト</button></li>
        </ul>
    </div>
</div>
```
さらにレイアウトを用途の div の中にこれらのマークアップを挿入していくことになる。

---


## 現状のコンポーネント化の手法 ##

---

### JS ###

Backbone.js の Backbone.View 等で特定の機能をもった要素をコンポーネント化

---

### CSS ###

OOCSS / BEM 等のメソドロジーを利用し、命名規則でスタイルの適用範囲をコンポーネント化

#### BEM メソドロジー

```html
<div class="media">
    <img class="media__image">
    <div class="media__body">
        <p class="media__text">テキスト</p>
    </div>
</div>
```

---

### 問題点 ###

- ライブラリ間の互換性がない
- メソドロジー間の互換性がない

どちらかの技術で作ったコンポーネントは、それら以外を利用したプロジェクトに再利用しづらい。

---

## Web Components による解決 ##

ライブラリやコンポーネントでやりくりしていたコンポーネント化をオリジナル要素として定義することができる。

```html
<my-pulldown></my-pulldown>

```

---


# Web Components の仕様 #

Web Components は単体の仕様ではなくて、4つの仕様で成立している。

1. Templates
1. Custom Elements
1. Shadow DOM
1. HTML Imports

--- 


## Templates ##

PHP における smarty や JS だと Underscore.js 等が提供するテンプレート機能を機能をブラウザのネイティブで提供する。
<templete> 内に必要なものを記述する。

- DOMとして取得し扱うことができる
- パースされても描画されたり、スクリプトが実行されない
- クローンして追加されることでそれぞれ実行される

描画されない不活性なテンプレート要素。

---

## Custom Elements ##

HTML として定義されていない要素を作ることができる。

- - プロパティ・メソッド・イベントも設定できる
- タグの名前にはハイフンを含むプリフィックスが必要
- 既存要素を拡張する場合は、 `is="*"` 属性を付与する

---

## Shadow DOM ##

WebCompnents 周りだと一番の目玉仕様。

- DOMに対してカプセル化を提供する技術
- Shadow DOM 内に記述された CSS については、他に影響も与えないし、与えられない。
（ iframe みたいに読み込んだ親から影響が受けないものができると考えるとわかりやすい）

---

## HTML Imports ##

独自に作ったコンポーネントを読み込む技術。

- `<script>` や `<link>` で JS / CSS を読み込むように html を読み込むことができる
- `onload` `onerror` のイベントハンドラがある
- CORS(Cross-Origin Resource Sharing)の制約も適用される
- async 属性もサポート

---


# 簡単な Web Compnents を作ってみる #

Custom Elements と Shadow DOM、Template を合わせてコンポーネントを作り、つくったコンポーネントを HTML Import で読み込むという流れ。
が、今日は、HTML Import までうまくいかなかったので、少し高度なものを解説します。

---

# ブラウザのサポート状況 #

- ◯ Chrome
- ◯ Firefox
- × Safari
- × IE

が、Safari は政治的な理由で ShadowDOM が削除される等ちょっと混乱。
が、各ブラウザベンダは実装を前向きに対応していくとのこと。


# おつかれさまでした
