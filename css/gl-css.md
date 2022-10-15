# CSSのガイドライン

- [CSSのガイドライン](#cssのガイドライン)
  - [前提](#前提)
    - [BEMのおさらい](#bemのおさらい)
      - [Block](#block)
      - [Element](#element)
      - [Modifier](#modifier)
  - [ファイル・ディレクトリ構成](#ファイルディレクトリ構成)
    - [baseフォルダ](#baseフォルダ)
      - [base/_normarize.scss](#base_normarizescss)
      - [base/_base.scss](#base_basescss)
    - [componentフォルダ](#componentフォルダ)
    - [moduleフォルダ](#moduleフォルダ)
    - [pageフォルダ](#pageフォルダ)
      - [_mixin.scss](#_mixinscss)
    - [_print.scss](#_printscss)
  - [命名規則](#命名規則)
    - [Modifierの指定方法](#modifierの指定方法)
    - [動的な状態変化](#動的な状態変化)
      - [`aria-*`などの標準的な属性セレクタ](#aria-などの標準的な属性セレクタ)
      - [Modifier](#modifier-1)
    - [メディアクエリ](#メディアクエリ)
    - [サフィックス（接尾辞）](#サフィックス接尾辞)
  - [フォーマッティング](#フォーマッティング)
    - [インポート](#インポート)
    - [フォーマットとプロパティの宣言順](#フォーマットとプロパティの宣言順)
      - [ルールセットのフォーマット](#ルールセットのフォーマット)
      - [単一行ルールセットのフォーマット](#単一行ルールセットのフォーマット)
      - [個別指定プロパティの宣言順](#個別指定プロパティの宣言順)
      - [カラーコードは短縮する](#カラーコードは短縮する)
      - [文字列には引用符（ダブルクォート）をつける](#文字列には引用符ダブルクォートをつける)
      - [0に単位をつけない](#0に単位をつけない)
      - [すべて小文字で記述する](#すべて小文字で記述する)
      - [ショートハンドはなるべく避ける](#ショートハンドはなるべく避ける)
      - [変数にはdefaultフラグを指定する](#変数にはdefaultフラグを指定する)
    - [セレクタ](#セレクタ)
      - [インライン記述を使用しない](#インライン記述を使用しない)
      - [HTMLの構造に依存させない](#htmlの構造に依存させない)
      - [IDセレクタを使用しない](#idセレクタを使用しない)
      - [メディアクエリをまとめて管理しない](#メディアクエリをまとめて管理しない)
      - [セレクタを短くする](#セレクタを短くする)
      - [divやspanをセレクタに使用しない](#divやspanをセレクタに使用しない)
    - [プロパティ・ルールセット](#プロパティルールセット)
      - [!importantを多用しない](#importantを多用しない)
      - [スタイルをリセットしない](#スタイルをリセットしない)
      - [要素セレクタに装飾的なスタイルを指定しない](#要素セレクタに装飾的なスタイルを指定しない)
      - [高さを指定しない](#高さを指定しない)
      - [固定の幅を持たせない](#固定の幅を持たせない)
      - [line-heightは単位をつけない](#line-heightは単位をつけない)
      - [font-size はremで指定する](#font-size-はremで指定する)
  - [印刷対応](#印刷対応)

## 前提
[BEM](http://getbem.com/)をベースにします。

また、SCSSにおいては`@import`は使わず、`@use`と`@forward`を使った[Dart Sass](https://sass-lang.com/dart-sass)を採用します。

### BEMのおさらい

BEMは、Block（大きな括り）・Element（ブロック内の要素）・Modifier（Block・Elementの亜種パターン）の頭文字をとったもので、厳格なクラス命名規則が特徴の手法です。
画面構成する要素を、この3つのどれかに当てはめてクラス名を付与していきます。

#### Block
構成要素となる大きなくくりです。ページ内で何度でもどこへでも置くことができる、独立して動作するものです。

#### Element
Blockに紐付いて定義されるものです。要素内のパーツであり、Block内であれば繰り返し使用できます。

```html
<!-- Block + Element -->
<div class="box">
  <div class="box__title">タイトル</div>
  <div class="box__text">テキスト</div>
</div>
```

#### Modifier
Block・Elementの亜種パターンです。少しだけ違うものを量産するときに用い、あくまで変更がかかる要素に対して付けます。

以下は構成要素自体の違い（`.box`に線をつける）を定義した例です。

```html
<!-- Block + Modifier -->
<div class="box box--border">
  <div class="box__title">タイトル</div>
  <div class="box__text">テキスト</div>
</div>
```
以下はElementのバリエーションを作る場合（タイトルの文字サイズを大きくする）の例です。

```html
<!-- Block + Element + Modifier -->
<div class="box">
  <div class="box__title box__title--big">タイトル</div>
  <div class="box__text">テキスト</div>
</div>
```

## ファイル・ディレクトリ構成
以下のようにファイルとフォルダを配置します。

```
scssフォルダ
├─ baseフォルダ：リセットとサイト共通定義
│  ├─ _base.scss：サイト共通定義
│  └─ _normalize.scss：リセットCSS
├─ componentフォルダ：サイト内で何度も使うデザイン定義群
│  ├─ _button.scss：ボタンデザイン
│  └─ _form.scss：フォームデザイン
├─ moduleフォルダ：ブロック単位のSCSSファイル群
│  ├─ _header.scss：ヘッダーデザイン
│  └─ _footer.scss：フッターデザイン
├─ pageフォルダ：ページ専用CSSが必要な時に使用するファイル群
│  └─ _about.scss
├─ _mixin.scss：サイト共通変数
├─ _print.scss：印刷用CSS
└─ style.scss
```

すべてのファイルはstyle.cssとして統合します。
大きくは4つのフォルダに分かれます。

- base
- component
- module
- page

### baseフォルダ
baseフォルダは要素セレクタのデフォルトスタイルやNormalize.cssなど、ベースになるスタイルを配置します。

#### base/_normarize.scss
[Normalize.css](https://necolas.github.io/normalize.css/)です。一般的なリセットCSSは`outline`プロパティを削除してしまうなどのデメリットもあるので、必要最小限の平準化だけをするNormalize.cssを使用します。

#### base/_base.scss
サイトを構成する上で、デザインの基本の下地、土台となるスタイルを定義します。  
あくまで土台ですので、ここでは装飾的なスタイルは定義せず、ブラウザのデフォルトスタイルシートやリセットCSSで指定されるような最低限のスタイルにとどめておきます。

- `p`や`em`など、HTMLタグ自体にスタイルを定義
- _normarize.scssで足りなかったリセットを追加
- 基本の文字サイズやフォントファミリーなどを追加

### componentフォルダ
繰り返し使われるサイト共通の小さな単位のパーツを管理します。例えば以下のようなものです。

- _button.scss
- _table.scss

### moduleフォルダ
サイト共通で使用するモジュール別にスタイルが定義さているSCSSファイルを格納します。  
moduleディレクトリに格納されるSCSSファイルは、必ずBEM設計のBlock単位になります。  
また、サイト共通で使用するモジュール（Block）となりますので、次のBlockは基本的にどの案件でも出てくるモジュールです。

- _header.scss：サイト共通ヘッダー
- _footer.scss：サイト共通フッター
- _sidebar.scss：サイドバー
- _content.scss：コンテンツ

ファイルを追加する際は、以下のルールを遵守します。

- 1つのBlockに対し1つの定義ファイルを作成する
- SCSSファイル名は`_Block名.scss`とする

### pageフォルダ
moduleで定義したスタイルの各ページにおける微調整など、専用CSSが必要なものを格納します。

#### _mixin.scss
サイト共通の変数やmixinを格納します。例えば以下のようなものです。

- ブレイクポイント
- 横幅の最大値
- フォントのサイズや種類
- 使用する色

### _print.scss
印刷用のCSSです。

## 命名規則
前述の「BEMのおさらい」に基づき、基本的には以下のような親子関係になります。

```
BlockName > ComponentName > ChildNode
```

### Modifierの指定方法
拡張された要素（Element + Modifier）をベースに、さらに拡張したスタイルを定義する場合、判別しにくいためModifierの連結は避けます。

```html
<!-- ベースのスタイル -->
<div class="box">
  <div class="box__title">タイトル</div>
</div>

<!-- 拡張した要素 -->
<div class="box box--white">
  <div class="box__title">タイトル</div>
</div>

<!-- Bad: Modifierを連結 -->
<div class="box box--white--big">
  <div class="box__title">タイトル</div>
</div>

<!-- Good: 1つのバリエーションとして再定義 -->
<div class="box box--whitebig">
  <div class="box__title">タイトル</div>
</div>

```

### 動的な状態変化
クリック時などの動的な状態変化があった場合は以下の優先度で指定してください。

1. `aria-*`などの標準的な属性セレクタ
2. Modifier

#### `aria-*`などの標準的な属性セレクタ
`aria-expanded`や`aria-hidden`のような属性を使用している場合は、CSSのセレクタにも使用してください。

```scss
.namespace-ModuleName_ChildNode {
  &[aria-expanded="true"] {
    ...
  }
}
```

#### Modifier
`aria-*`などの属性がつけられない場合は、Modifierを指定してください。

```scss
.namespace-ModuleName_ChildNode {
  &--Modifier {
    ...
  }
}
```

### メディアクエリ
PCデザインから作成する都合上、PCファーストで記述します。また、メディア特性はスクリーンだけでなく印刷も指定します。

```scss
@media print, screen and (max-width: 768px) {}
```

### サフィックス（接尾辞）
ブレイクポイントで変化するクラス名はサフィックスで表します。
サフィックスで使用するキーワードは変数のキーを使います。

```scss
$breakpoint-up: (
  'sm': 'print, screen and (min-width: 375px)',
  'md': 'print, screen and (min-width: 768px)',
  'lg': 'print, screen and (min-width: 1024px)',
  'xl': 'print, screen and (min-width: 1440px)',
) !default;
```

```scss
@include mq-up(md) {
  .l-Grid_Item {
    &-1of12Md { width: percentage(1 / 12)};
    &-2of12Md { width: percentage(2 / 12)};
    &-3of12Md { width: percentage(3 / 12)};
    &-4of12Md { width: percentage(4 / 12)};
    &-5of12Md { width: percentage(5 / 12)};
    &-6of12Md { width: percentage(6 / 12)};
    &-7of12Md { width: percentage(7 / 12)};
    &-8of12Md { width: percentage(8 / 12)};
    &-9of12Md { width: percentage(9 / 12)};
    &-10of12Md { width: percentage(10 / 12)};
    &-11of12Md { width: percentage(11 / 12)};
    &-12of12Md { width: percentage(12 / 12)};
  }
}
```

## フォーマッティング
### インポート
ファイルの呼び出し方として、`@use`と`@forward`の2つがあります。この2つには以下の違いがあります。

- `@use`を記述してあるファイルを読み込んだときに、ファイルの内容が引き継がれない（継承が発生しない）
- `@use`でファイルを読み込んだら、変数や`mixin`を使う時に、どのファイルのものかを明示するため、名前空間を指定する必要がある。

ややこしいため、WordPressベーステーマでは変数や`mixin`を`_mixin.scss`で一括管理し`@use`を利用しています。

### フォーマットとプロパティの宣言順
CSSの構文はセレクタとブレース、プロパティと値で構成されます。このルールセットに読みやすさを確保したフォーマット（書式）をルール化します。

#### ルールセットのフォーマット
ルールセットの基本的なフォーマットは以下の通りです。

- 複数のセレクタは別の行に（関連性があって1行が長くなり過ぎなければ同じ行に指定してもいい）
- 最後のセレクタとオープニングブレースの間にスペースを1つ
- それぞれの宣言は別々の行に
- ルールセット内に空行は入れない
- プロパティの前にインデントとしてスペースを2つ
- コロン（`:`）と値の間にスペースを1つ
- 各ルールセットの間に空行を1つ
- 関数はカンマ（`,`）と引数の間にスペースを1つ
- ローカル変数は最初に定義
- extendはローカル変数の次に指定
- mixinはextendの次に指定
- contentを使用しているmixinは適切な位置に指定
- 演算は常に括弧（`()`）で囲む
- 括弧内のカンマ（`,`）と値の間にスペースを1つ
- メディアクエリや擬似要素など別のセレクタが生成される場合は空行を1つ

```scss
// Good
.Foo, .Foo--Bar,
.Baz {
  $padding: 1em;
  @extend %base-unit;
  @include clearfix;
  display: block;
  margin-right: auto;
  margin-left: auto;
  padding-right: $padding;
  padding-left: $padding;
  backgrouond-color: rgba(0, 0, 0, 0.7);

  @include mq-up(md) {
    padding-right: ($padding * 2);
    padding-left: ($padding * 2);
  }
}

// Bad
.Foo,
.Foo--Bar, .Baz{
    @include mq-up(md) {
        padding-right: $padding * 2;
        padding-left: $padding * 2;
  }
    display: block;margin-right: auto;
    backgrouond-color: rgba(0,0,0,0.7);
    margin-left:auto;
    @extend %base-unit;
    @include clearfix;
    $padding: 1em;}
```

#### 単一行ルールセットのフォーマット
原則的には複数行でルールセットを記述しますが、単一のスタイルの場合は1行で記述することもできます。

単一行のフォーマットは以下の通りです。

- 最後のセレクタとオープニングブレースの間にスペースを1つ
- オープニングブレースとプロパティの間にスペースを1つ
- コロン（`:`）と値の間にスペースを1つ
- セミコロン（`;`）とクロージングブレースの間にスペースを1つ
- 各ルールセットの間には空行を入れない

```scss
// Good
.Grid_Item-col2 { width: percentage(1 / 2); }
.Grid_Item-col3 { width: percentage(1 / 3); }
.Grid_Item-col4 { width: percentage(1 / 4); }
```

#### 個別指定プロパティの宣言順
`margin`や`position`のように上下左右に個別に指定できるプロパティは時計回り（上・右・下・左）で記述をすることで規則性をもたせます。

```scss
// Good
.Foo {
  margin-top: 30px;
  margin-right: auto;
  margin-left: auto;
}

// Bad
.Foo {
  margin-left: auto;
  margin-right: auto;
  margin-top: 30px;
}
```

#### カラーコードは短縮する
colorプロパティなどで色を指定する時は可読性をあげるために、可能な場合は短縮します。

```scss
// Good
.Foo { color: #ddd; }

// Bad
.Foo { color: #dddddd; }
```

#### 文字列には引用符（ダブルクォート）をつける
contentプロパティやURLの指定、属性セレクタの指定をする時にはダブルクォートを使用します。

```scss
// Good
.Foo {
  content: "this is content";
  background: url("logo.png");
}
input[type="submit"] {}

// Bad
.Foo {
  content: 'this is content';
  background: url(logo.png);
}
input[type=submit] {}
input[type='submit'] {}
```

#### 0に単位をつけない
値が`0`の場合は`px`や`%`といった単位は必要がないため指定しません。

```scss
// Good
.Foo { margin: 0; }

// Bad
.Foo { margin: 0px; }
```

ただし、角度（`deg`,`grad`,`rad`,`turn`）や時間（`s`,`ms`）では単位の省略をすることができないので注意します。

#### すべて小文字で記述する
プロパティとプロパティ値は大文字でも小文字でも同様に扱われますが、小文字で統一します。

```scss
// Good
.Foo { color: #fff; }

// Bad
.Foo { COLOR: #FFF; }
```

#### ショートハンドはなるべく避ける
`font-size`や`margin`などのショートハンドプロパティの使用は必要がなければ避けます。ショートハンドプロパティに渡さなかったプロパティに初期値が指定されてしまい、思わぬスタイルが当たってしまう恐れがあるためです。

必要なプロパティにだけ指定するほうがコードの意図もわかりやすくなります。

```scss
// Good
.Foo {
  // 中央配置にする。
  margin-right: auto;
  margin-left: auto;
}

// Bad
// 上下を0に指定する必要がない。
.Foo { margin: 0 auto; }
```

#### 変数にはdefaultフラグを指定する
変数を定義するときには`!default`フラグも指定します。同じ変数名の場合、先に定義した変数が適応されるというシンプルなルールになるので管理がしやすくなります。

```scss
// Good
$unit-base: 1em !default;

// Bad
$unit-base: 1em;
```

### セレクタ
#### インライン記述を使用しない
HTMLのstyle属性にスタイルを記述することを避けます。HTMLには見た目に関する情報を極力書かないようにします。クラスを振ったほうが柔軟にスタイルを変更することができます。JavaScriptを使う場合もstyle属性を避けてください。

```html
<!-- Bad -->
<div style="color:red; background-color: black;"></div>
```

#### HTMLの構造に依存させない
要素セレクタに対してスタイルを指定すると、HTMLの構造が変更されたときにスタイルが崩れてしまう恐れがあります。

```scss
// Bad
article h2 {}
```

クラスセレクタであれば指定している要素に関係なくスタイルが適応されるので、使い回しがしやすくなります。ただし、要素（例えば`ul`と`div`）によってデフォルトのスタイルが違うことがあるので、スタイルが崩れないようにリセットしておく必要がある場合があります。

```html
<ul class="ns-Grid">
</ul>

<div class="ns-Grid">
</div>
```

クラスセレクタに対して要素セレクタを連結させるのも避けます。詳細度が上がってしまい、上書き時に`!important`を使わざるを得なくなる場合があるためです。

```scss
// Good
.Foo {}

// Bad
h2.Foo {}
```

特定の要素で指定してほしいのであれば、コメントやクラス名でそれを示します。

```scss
// Good
/* ulタグかolタグに指定してください。 */
.Foo {}
```

#### IDセレクタを使用しない
CSSセレクタにIDセレクタは使用しません。ページ内リンクやJavaScriptのフックとしてだけ使います。

#### メディアクエリをまとめて管理しない
メディアクエリをまとめて指定しません。そのモジュールがどのように変化していくのかを把握しにくくしてしまいます。

```scss
// Good
.Foo {}

@media (min-width: 768px) {
  .Foo {}
}

// Bad
.Foo {}
.Bar {}
.Baz {}

@media (min-width: 768px) {
  .Foo {}
  .Bar {}
  .Baz {}
}
```

#### セレクタを短くする
セレクタは必ずしもHTML構造に沿う必要はありません。場合によってはセレクタを短くすることで詳細度を低く抑えることができます。

```scss
// Good
ul a {}
th {}

// Bad
ul li a {}
table th {}
```

#### divやspanをセレクタに使用しない
`div`や`span`は使用頻度が高く、パターンも一定ではありません。セレクタに指定すると意図しないところにスタイルが当たってしまう恐れがあります。`div`と`span`にはスタイルを指定せずに、クラスを振って指定します。

```scss
// Good
.Foo_ChildNode {}

// Bad
div {}
span {}
.Foo div {}
.Foo span {}
```

### プロパティ・ルールセット
#### !importantを多用しない
`!important`の使用は禁止しませんが、多用するべきではありません。そのモジュール内で完結する場合にだけ使用してください。

#### スタイルをリセットしない
スタイルのリセットとは、`0`や`none`などで値を上書きすることです。スタイルのリセットが多いときは、要素にスタイルを持たせすぎていたり、早く指定しすぎている恐れがあります。

```scss
// Bad
.Foo {
  border: 1px solid #ddd;
}

// ある要素内ではボーダーが邪魔になるためリセット
.Bar .Foo {
  border: none;
}
```

Modifierで必要なときにだけ指定するとリセットが起きにくくなります。

```scss
// Good
.Foo {}
.Foo--bordered {
  border: 1px solid #ddd;
}
```

#### 要素セレクタに装飾的なスタイルを指定しない
`h1`や`p`といったセマンティックな要素セレクタには多くのスタイル（特に装飾的なスタイル）を指定しません。必ずあとでスタイルをリセットすることになります。

```scss
// Bad
h2 {
  padding-bottom: 0.5em;
  border-bottom: 1px solid #888;
}
```

要素セレクタにはブラウザのデフォルトスタイルシートやリセットCSSで指定されるような最低限のスタイルにとどめておきます。

```scss
// Good
h2 {
  font-size: 2rem;
  line-height: 1.2;
  margin-top: 0;
  margin-bottom: 24px;
}
```

#### 高さを指定しない
レスポンシブでは横幅も高さも環境に応じて変化します。高さを固定していると余分な余白ができてしまったり、逆にコンテンツが隠れてしまう恐れがあります。

```scss
// Bad
.Foo {
  height: 300px;
}
```

#### 固定の幅を持たせない
コンテンツは基本的に親要素に対して横幅100%の表示になるようにします。横幅を固定すると横幅が足りなかったり、はみ出してしまう恐れがあります。

幅を変更するときは、コンテナブロックに`max-width`を指定する、`width`のヘルパークラスを指定する、Modifierでサイズを指定するなどの方法があります。

```scss
// Good
.sw-Button {}

.l-Wrapper {
  max-width: 1200px;
}

.sw-Button-full {
  width: 100%;
}

.Grid_Item-col2 { width: percentage(1 / 2); }
.Grid_Item-col3 { width: percentage(1 / 3); }
.Grid_Item-col4 { width: percentage(1 / 4); }

// Bad
.sw-Button {
  width: 300px;
}
```
#### line-heightは単位をつけない
単位を指定すると、親要素で計算された値が子要素、孫要素に継承されてしまいます。

#### font-size はremで指定する
`rem`はルート（`html`）のフォントサイズを1として考える相対的な単位です。
デバイスによってフォントサイズを変える場合などを考え、`px`は使用しないでください。

WordPressベーステーマでは 1rem は 10px になります。


## 印刷対応
特に要望がない限りは特別な対応はしないものとします。  
印刷対応の要望があった場合は _print.scss に記述します。