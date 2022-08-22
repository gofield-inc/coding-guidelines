# CSSのガイドライン

- [CSSのガイドライン](#cssのガイドライン)
  - [前提](#前提)
  - [ファイル・ディレクトリ構成](#ファイルディレクトリ構成)
    - [foundationフォルダ](#foundationフォルダ)
      - [foundation/_normarize.scss](#foundation_normarizescss)
      - [foundation/_base.scss](#foundation_basescss)
    - [layoutフォルダ](#layoutフォルダ)
      - [layout/l-container.scss](#layoutl-containerscss)
    - [objectフォルダ](#objectフォルダ)
      - [object/componentフォルダ](#objectcomponentフォルダ)
      - [object/projectフォルダ](#objectprojectフォルダ)
      - [_mixins.scss](#_mixinsscss)
    - [_print.scss](#_printscss)
  - [命名規則](#命名規則)
    - [variantの指定方法](#variantの指定方法)
    - [状態変化](#状態変化)
      - [`aria-*`などの標準的な属性セレクタ](#aria-などの標準的な属性セレクタ)
      - [variant](#variant)
    - [メディアクエリ](#メディアクエリ)
    - [サフィックス（接尾辞）](#サフィックス接尾辞)
    - [キーセレクタ](#キーセレクタ)
  - [スタイルガイド](#スタイルガイド)
  - [フォーマッティング](#フォーマッティング)
    - [インポート](#インポート)
    - [フォーマットとプロパティの宣言順](#フォーマットとプロパティの宣言順)
      - [ルールセットのフォーマット](#ルールセットのフォーマット)
      - [単一行ルールセットのフォーマット](#単一行ルールセットのフォーマット)
      - [プロパティの宣言順](#プロパティの宣言順)
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

## 前提
[Foundation Layout Object CSS](https://github.com/hiloki/flocss)（FLOCSS）をベースにします。
FLOCSSは[OOCSS](https://www.slideshare.net/stubbornella/object-oriented-css)や[BEM](http://getbem.com/)、[SMACSS](https://smacss.com/)のいいとこ取りをしたCSS設計思想です。

FLOCSSを使うメリットは以下の通りです。

- CSSがコンポーネント化されるため、再利用や修正に強くなる
- BEMのネーミングルールによってクラスの役割が明確化される
- 全体として管理のしやすいソースコードが出来上がる

また、SCSSにおいては@importは使わず、@useと@forwardを使ったDart Sassを採用します。

## ファイル・ディレクトリ構成
以下のようにファイルとフォルダを配置します。

```
scssフォルダ
├─ foundationフォルダ：リセットとサイト共通定義
│  ├─ _base.scss：サイト共通定義
│  └─ _normalize.scss：リセットCSS
├─ componentsフォルダ：サイト内で何度も使うデザイン定義群
│  ├─ _button.scss：ボタンデザイン
│  └─ _form.scss：フォームデザイン
├─ moduleフォルダ：ブロック単位のSCSSファイル群
│  ├─ _layout.scss：レイアウトデザイン
│  └─ _header.scss：ヘッダーデザイン
├─ pagesフォルダ：ページ専用CSSが必要な時に使用するファイル群
│  └─ _top.scss：トップページ用デザイン定義
├─ _mixins.scss：サイト共通変数
├─ _print.scss：印刷用CSS
└─ style.scss
```

すべてのファイルはstyle.cssとして統合します。
大きくは4つのフォルダに分かれます。

- foundation
- components
- module
- pages

### foundationフォルダ
baseフォルダは要素セレクタのデフォルトスタイルやNormalize.cssなど、ベースになるスタイルを配置します。

#### foundation/_normarize.scss
[Normalize.css](https://necolas.github.io/normalize.css/)です。一般的なリセットCSSは`outline`プロパティを削除してしまうなどのデメリットもあるので、必要最小限の平準化だけをするNormalize.cssを使用します。

#### foundation/_base.scss
サイトを構成する上で、デザインの基本の下地、土台となるスタイルを定義します。

- `p`や`em`など、HTMLタグ自体にスタイルを定義
- _normarize.scssで足りなかったリセットを追加
- 基本の文字サイズやフォントファミリーなどを追加

### layoutフォルダ
各ページを構成する、ヘッダー、メインコンテンツエリア、コンテナ、フッターなどのレイアウトに関するスタイルをエリアごとに管理します。

- 位置など、レイアウトの指定のみ定義
- 子要素は入れない
- 自身のデザインはprojectフォルダで定義する

#### layout/l-container.scss
サイトのメインエリア内のコンテンツ幅、左右の余白の指定

### objectフォルダ
パーツやブロックをすべて object と定義。

- 小さな単位のパーツを Component に。
- Componentが集まったブロックや、大きなエリアは Project に。

#### object/componentフォルダ
繰り返し使われるサイト共通の小さな単位のパーツを管理します。例えば以下のようなものです。

- c-button.scss
- c-label.scss
- c-input.scss

#### object/projectフォルダ
いくつかの component と要素によって構成される、大きなブロックやエリアを管理。

- ヘッダやフッタなどのオブジェクト
- 小さい単位のcomponentを集めて、一つのオブジェクトとして扱いたい時
- componentとするには大きすぎるもの

例
- p-card.scss
- p-first-view.scss
- p-button-group.scss

<!-- ### pagesフォルダ
デザインカンプがあるページなど、専用CSSが必要なものを格納します。
しかし、最終的にはstyle.cssに統合され全てのページで読み込まれるため、別のページでも使い回せるように留意します。 -->

#### _mixins.scss
サイト共通の変数を格納します。例えば以下のようなものです。

- ブレイクポイント
- 横幅の最大値
- フォントのサイズや種類
- 使用する色

### _print.scss
印刷用のCSSです。

## 命名規則
命名規則は[BEM](http://getbem.com/)の考えをベースにします。

BEMは、Block（大きな括り）・Element（ブロック内の要素）・Modifier（Block・Elementの亜種パターン）の頭文字をとったもので、厳格なクラス命名規則が特徴の手法です。
画面構成する要素を、この3つのどれかに当てはめてクラス名を付与していきます。

```scss
.Block__element--modifier {}
// .namespace-ModuleName_ChildNode-variant {}
// .namespace-ComponentName_ChildNode-variant {}
```

基本的には以下のような親子関係になります。

```
ModuleName > ComponentName > ChildNode
```

ただし、名前からはModuleNameなのかComponentNameなのかは判断できないことも多いのでそれほど気にする必要はありません。

### variantの指定方法
variantはChildNodeに指定してもいいですが、HTMLでの管理がしにくい場合はModuleNameやComponentNameに指定することも検討してください。

```scss
.namespace-ModuleName_ChildNode {
  ...
}

// ChildNodeをChildNode-variantで上書きする
.namespace-ModuleName_ChildNode-variant {
  ...
}
```

```scss
.namespace-ModuleName_ChildNode {
  ...

  // ChildNodeをModuleName-variantで上書きする
  .namespace-ModuleName-variant & {
    ...
  }
}
```

### 状態変化
クリック時などの動的な状態変化があった場合は以下の優先度で指定してください。

1. `aria-*`などの標準的な属性セレクタ
2. variant

#### `aria-*`などの標準的な属性セレクタ
`aria-expanded`や`aria-hidden`のような属性を使用している場合は、CSSのセレクタにも使用してください。

```scss
.namespace-ModuleName_ChildNode {
  .namespace-ModuleName[aria-expanded="true"] & {
    ...
  }
}
```

#### variant
`aria-*`などの属性がつけられない場合は、variantを指定してください。

```scss
.namespace-ModuleName_ChildNode {
  .namespace-ModuleName-expanded & {
    ...
  }
}
```

### メディアクエリ
メディアクエリは`min-width`を指定してモバイルファーストで記述します。また、メディア特性はスクリーンだけでなく印刷も指定します。

```scss
@media print, screen and (min-width: 768px) {}
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

ブレイクポイントでの変化のパターンが1つに決まっている場合はCSSだけで完結させます。

### キーセレクタ
あるセレクタのルールセット（`{}`）の中に、他のキーセレクタ（実際に適応されるセレクタ）が入らないようにしてください。

`.Foo`の中に`.Bar`が入っているのでNG。

```scss
.Foo {
  ...

  & .Bar {
    ...
  }
}
```

キーセレクターは`.Bar`なので、`.Bar`のルールセットの中に指定します。

```scss
.Bar {
  ...

  .Foo & {
    ...
  }
}
```

また、以下のようにルールセット内に他のキーセレクターを生成するのもNGです。

```scss
.Foo {
  ...

  &_Bar {
    ...
  }
}
```

1つのルールセットの中でキーセレクターを閉じ込めるようにします。

```scss
.Foo {
  ...
}

.Foo_Bar {
  ...
}
```

## スタイルガイド
下層ページのデザインデータに基づき、まずはスタイルガイドにデザインを適用します。

- a-blog.cms/_templates/styleguide.html
- wordpress/styleguide/

## フォーマッティング
### インポート
Sassの`@import`でパーシャルファイルをインポートするときは、Globパターンでインポートして、コメントに使用している名前空間の説明を載せます。

```scss
@charset "UTF-8";

@import "base/variable/**/*.scss";
@import "base/function/**/*.scss";
@import "base/mixin/**/*.scss";
@import "base/_normalize.scss";
@import "base/_base.scss";

/**
 * .sw- (SiteWide)...サイト共通の汎用的なModule（リストやボタンなどの場所を選ばないもの）
 * .st- (Structure)...サイト共通の構造的なModule（ヘッダーやフッターのような場所が固定されるもの）
 * .l- (Layout)...コンテンツ内の余白やレイアウト専用のModule
 * .wisywig- (WISYWIG)...WISYWIG（ウィジウィグ）で入力した要素に対するスタイル
 * .home- (HomePage)...ホームページ（サイトトップページ）
 * .top- (TopPage)...カテゴリートップページ
 * .sub- (SubPage)...カテゴリー下層ページ
 * .products- (Products)...製品情報
 * .news- (News)...ニュース
 * .company- (Company)...会社案内・企業情報
 * .recruit- (Recruit)...採用情報ページ
 * .csr- (CorporateSocialResponsibility)...企業の社会的責任
 * .faq- (FrequentlyAskedQuestions)...よくある質問
 * .inquiry- (Inquiry)...お問い合わせ
 * .ir- (InvestorRelations)...投資家向け情報
 * .results- (Results)...検索結果ページ
 * .sitemap- (Sitemap)...サイトマップページ
 */
@import "namespace/**/*.scss";

@import "_print.scss";
```

### フォーマットとプロパティの宣言順
CSSの構文はセレクタとブレース、プロパティと値で構成されます。このルールセットに読みやすさを確保したフォーマット（書式）をルール化します。

#### ルールセットのフォーマット
ルールセットの基本的なフォーマットは以下の通りです。

- 複数のセレクタは別の行に（関連性があって1行が長くなり過ぎなければ同じ行に指定してもいい）
- 最後のセレクタとオープニングブレースの間にスペースを1つ
- それぞれの宣言は別々の行に
- ルールセット内に空行は入れない
- プロパティの前にスペースを2つ
- コロン（`:`）と値の間にスペースを1つ
- クロージングブレースは独立した行に
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

#### プロパティの宣言順
ルールセット内の宣言は重要なプロパティから書き始め、その機能ごとに固めて記述することで意図を素早く理解できるようにします。プロパティの宣言順は以下のようなルールで記述します。

- ボックスモデルの種類や表示方法を示すプロパティ（`box-sizing`, `display`, `visibility`, `float`など）
- 位置情報に関するプロパティ（`position`, `z-index`など）
- ボックスモデルのサイズに関するプロパティ（`width`, `height`, `margin`, `padding`, `border`など）
- フォント関連のプロパティ（`font-size`, `line-height`など）
- 色に関するプロパティ（`color`, `background-color`など）
- それ以外

書きやすさと読みやすさを考えてアルファベット順では書きません。例えばアルファベット順では`position`プロパティで位置の指定をする場合に`top`と`left`が離れてしまい、読みにくくなってしまいます。

```scss
// Good
.Foo {
  display: block;
  position: absolute; // 親要素に対して、
  top: 0;
  left: 0; // 左上を基準にする。
  width: 100%;
  margin: 0;
  padding: 0;
  font-size: 0.75em;
  color: #000;
  background-color: #fff;
}

// Bad
.Foo {
  background-color: #fff;
  color: #000;
  display: block;
  font-size: 0.75em;
  left: 0; // どこかにpositionがある？
  margin: 0;
  padding: 0;
  position: absolute; // positionがあった、親要素を基準にするのか
  top: 0; // 上にあわせて、他の値はなんだっただろう？
  width: 100%;
}
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
`font-size`や`margin`などのショートハンドプロパティの使用は必要がなければ避けます。ショートハンドプロパティに渡さなかったプロパティに初期値が指定されてしまい、思わぬスタイルが当たってしまう恐れがあるからです。

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

クラスセレクタであれば指定している要素に関係なくスタイルが適応されるので、使い回しがしやすくなります。ただし、要素（例えば`ul`と`div`）によってデフォルトのスタイルがちがうことがあるので、スタイルが崩れないようにリセットしておく必要がある場合があります。

```html
<ul class="ns-Grid">
</ul>

<div class="ns-Grid">
</div>
```

クラスセレクタに対して要素セレクタを連結させるのも意味がありません。

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

※上記は推奨ではなく例です。`ul a`のようなセレクタを使用してもいいというわけではありません。

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

variantで必要なときにだけ指定するとリセットが起きにくくなります。

```scss
// Good
.Foo {}
.Foo-bordered {
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

幅を変更するときは、コンテナブロックに`max-width`を指定する、`width`のヘルパークラスを指定する、variantでサイズを指定するなどの方法があります。

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