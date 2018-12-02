# [チュートリアル：React事始め](https://reactjs.org/tutorial/tutorial.html)

このチュートリアルでは、既存のReact知識は想定していません。

## チュートリアルを始める前に / Before We Start the Tutorial

このチュートリアルでは小さなゲームを作ります。
**ゲームを作りたいわけではないから飛ばしてしまおうと思うかもしれませんが、それでも試してみてください。**
このチュートリアルを通して習得する技術は、様々なReactアプリを作るための基礎的なものであり、マスターすることでReactについて深い理解を得られるでしょう。

>Tips<br>
>このチュートリアルは、手を動かして学ぶことを好む人向けに作られています。

チュートリアルはいくつかのセクションに分かれています。

- **セットアップ** チュートリアルを開始するための準備。
- **概要** Reactの基礎。components, pros, state.
- **ゲームを完成させる** React開発における最も基礎的な技術。
- **タイムトラベルの追加** Reactが得意なことについてのより深い理解。

一度でチュートリアルを完了する必要はありません。１セクションずつでも、無理のない速度で学習しましょう。

チュートリアルはコピペでも動くようになっていますが、手打ちで進めることを推奨します。
体で覚え、深い理解を得るにはそれが一番です。

### 何を作るのか？ / What Are We Building?

インタラクティブなtic-tac-toeゲーム[^1]をReactで作ります。

最終的な結果を[こちら](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)で確認することができます。
もし今の段階でコードが理解できなかったり、文法に親近感を感じなくても、心配はいりません。
チュートリアルを完了する頃には、きっとReactと文法を理解できるでしょう。

チュートリアルを続ける前に、tic-tac-toeゲームを遊んでみることをお勧めします。
あなたが注意すべき特徴の一つは、番号付きリストがゲームボードの右側に表示されていることでしょう。
このリストはあなたにゲーム中に起きた全ての手の履歴をあなたに提示し、ゲームの進行にあわせて更新されます。

tic-tac-gameがどういうゲームかを理解したら終了しましょう。
このチュートリアルでは、シンプルなテンプレートから始めます。
次のステップは、あなたがゲームを作れるようにすることです。

[^1]: 三目並べ

### 前提条件 / Prerequisites

我々はあなたが多少はHTMLとJavaScriptに親しんでいることを想定していますが、別のプログラミング言語のみに親しんでいた場合でもそれほど問題はないはずです。
また、あなたがプログラミングにおける関数、オブジェクト、配列、小規模なクラス、くらいのプログラミングの概念に親しんでいることを想定しています。

もしJavaScriptについて確認したいことがあるなら、[このガイド](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)を読むことをお勧めします。
また、我々はES6（JavaScriptの最近のバージョン）のいくつかの機能を使用します。
このチュートリアルでは、アロー関数、classes、let、const の文法を使用します。
[Babel REPL](https://babeljs.io/repl/#?presets=react&code_lz=MYewdgzgLgBApgGzgWzmWBeGAeAFgRgD4AJRBEAGhgHcQAnBAEwEJsB6AwgbgChRJY_KAEMAlmDh0YWRiGABXVOgB0AczhQAokiVQAQgE8AkowAUAcjogQUcwEpeAJTjDgUACIB5ALLK6aRklTRBQ0KCohMQk6Bx4gA)を使用すれば、どのようなES6コードがコンパイルされるか確認できます。

## セットアップ / Setup for the Tutorial

チュートリアルを進めるにあたって、次のふたつの方法があります。

### 方法１：ブラウザ上でコーディング / Setup Option 1: Write Code in the Browser

訳者はこの方法使わないので飛ばします

### 方法２：ローカル開発環境 / Setup Option 2: Local Development Environment

1. 最新のNode.jsをインストールします
2. CreateReactAppで新しいプロジェクトを作成します
```
npm install -g create-react-app
create-react-app my-app
```
3. プロジェクトのsrc/フォルダ以下の全ファイルを削除します
```
cd my-app
rm -f src/*
```
4. [このCSSコード](https://codepen.io/gaearon/pen/oWWQNa?editors=0100)をindex.cssとしてsrc/直下に保存します。
5. [このJSコード](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)をindex.jsとしてsrc/直下に保存します。
6. 以下3行をindex.jsの先頭に記述します。
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
```
プロジェクトフォルダ内で run npm start を実行し、ブラウザから http://localhost:3000 を開けば、空の tic-tac-toe フィールドが表示されるでしょう.

[この導入](https://babeljs.io/docs/en/editors/)に従って、あなたのエディターにシンタックスハイライトを導入することをお勧めします。

### もし途中で行き詰まったら / Help, I’m Stuck!

もし行き詰まったら「community support resources」を確認するのが良いでしょう。
特に「Reactiflux Chat」はあなたが素早く助けを得る最も良い方法です。
もし答えを得られなかった、または問題が解決しなかった場合は、我々に問題を送ってくだされば解決しましょう。

## 概要 / Overview

いよいよ準備も終わって、これからが本番です。

### What is React?

Reactはユーザーインターフェースを構築するための、宣言的に書け、効率的に動作し、柔軟性に富んだJavaScriptライブラリです。
「components」と呼ばれる小さく独立したコードを合成することによって、複雑なUIを作ることができます。

## スターターコードの検査 / Inspecting the Starter Code

Reactはいくつかの異なる種類のcomponentsを持っていますが、今回はReact.Componentのサブクラスを使用します。

```
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// Example usage: <ShoppingList name="Mark" />
```

すぐにXML風の面白いタグに気付いたと思います。
これはcomponentsを使って、どう表示したいかをReactに伝えています。
これによりReactは、データが変更された時に、効率的な更新と、componentsのレンダリングを実現します。

このShoppingListはReact component class、またはReact component typeです。
componentはprops（propertiesの略）と呼ばれるパラメータを内部に取り込み、renderメソッドの戻り値としてview描画の階層を返却します。

renderメソッドはあなたがどうレンダリングしたいかの詳細を返却します。
Reactはそれを受け取り、その結果を表示します。
特にrenderメソッドが返却するのは、軽量なレンダリング情報であるReact elementです。
ほとんどのReact開発者達は、これらの構造を容易に記述できる、JSXと呼ばれる特別な構文を使います。
JSXで記述した <div /> 構文は、ビルド時に React.createElement('div') に変換されます。
先ほどの例と、下の例は同じレンダリング結果をもたらします。

```
return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
```

[see full expanded version](https://babeljs.io/repl/#?presets=react&code_lz=DwEwlgbgBAxgNgQwM5IHIILYFMC8AiJACwHsAHUsAOwHMBaOMJAFzwD4AoKKYQgRlYDKJclWpQAMoyZQAZsQBOUAN6l5ZJADpKmLAF9gAej4cuwAK5wTXbg1YBJSswTV5mQ7c7XgtgOqEETEgAguTuYFamtgDyMBZmSGFWhhYchuAQrADc7EA)

もし createElement() に興味をもったなら、[API reference](https://reactjs.org/docs/react-api.html#createelement)に詳しい説明がありますが、このチュートリアルでは必要ありません。
代わりに、[JSX](https://reactjs.org/docs/introducing-jsx.html)は引き続き使用します。

JSXにはJavaScriptのフルパワーがあります。
JSXの括弧の内側にはあらゆるJavaScriptを記述できます。
ReactElementは変数に格納でき、プログラム内で受け渡し可能なJavaScriptオブジェクトです。

ShoppingListコンポーネントは内包された<div /\>や<li /\>といったDOMコンポーネントを単にレンダリングするものです。
あなたは同じようにしてカスタムReactコンポーネントを作成し、レンダリングすることができます。
例えば、<ShoppingList /> と記述することで、ショッピングリストを参照することができます。
各Reactコンポーネントはカプセル化され、独立して操作できます。これがシンプルなコンポーネント群から複雑なUIを構築することを可能にしています。

### Propsを使ったデータの受け渡し / Passing Data Through Props

手始めに、BoardコンポーネントからSquareコンポーネントにデータを受け渡してみましょう。
BoardのrenderSquareメソッドのコードを、引数で渡されたpropsをSquareに渡すように変更します。

```
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
```

Squareコンポーネントのrenderメソッドを {/\* TODO \*/} で書かれたところを {this.props.value} に置き換え、先ほどの値を表示するように修正します。

```
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```

変更前：

<img width="250" alt="Before screenshot" src="https://reactjs.org/static/tictac-empty-1566a4f8490d6b4b1ed36cd2c11fe4b6-a9336.png">

変更後：レンダリングされた結果、各四角形の中に数値が表示されるようになったはずです。

<img width="250" alt="After screenshot" src="https://reactjs.org/static/tictac-numbers-685df774da6da48f451356f33f4be8b2-be875.png">

[View the full code at this point](https://codepen.io/gaearon/pen/aWWQOG?editors=0010)

おめでとう！
あなたは親のBoardコンポーネントから子のSquareコンポーネントに「propを受け渡す」ことができました。
親から子へのpropsの受け渡しは、Reactアプリにおいて情報が移動するための方法です。

### 対話的なコンポーネントの作成 / Making an Interactive Component

クリックしたらSquareコンポーントを”X”で埋めるようにしましょう。
まず、Squareコンポーネントのrenderメソッドで返却されるボタンタグを変更します。

```
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={function() { alert('click'); }}>
        {this.props.value}
      </button>
    );
  }
}
```

これでSquareをクリックすると、ブラウザ上にアラートが表示されるでしょう。


>Note:  
タイプ数を節約し、動作をわかりやすくするため、今後は以下のようにしてアロー関数をイベントハンドラに使用します。
```
class Square extends React.Component {
 render() {
   return (
     <button className="square" onClick={() => alert('click')}>
       {this.props.value}
     </button>
   );
 }
}
```
`onClick={() => alert('click')}` これは、onClick propに関数を渡していることに注意してください。
それはクリック後にのみ発生します。`()=>` を忘れ、 `onClick={alert('click')}` と書いてしまうのはよくあるミスで、そうするとcomponentがレンダリングされる度にalertを発生させます。

次のステップでは、Squareコンポーネントにクリックされたことを”覚えておいて”もらい、”X”マークを表示させる。
”覚えておいて”とはつまり、コンポーネントがstateを使うということだ。

Reactコンポーネントはコンストラクタで`this.state`を設定することで状態を保持することができる。
`this.state`は定義されたReactコンポーネントの中でprivateとなる。
現在の値をSquareコンポーネントの`this.state`に保管し、Squareがクリックされたら変更する。

まず、コンストラクタをSquareコンポーネントのクラスに定義し、stateを初期化する。

```
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button className="square" onClick={() => alert('click')}>
        {this.props.value}
      </button>
    );
  }
}
```

>Note
JavaScriptのクラスでは、サブクラスのconstructorを定義する時には必ずsuperをコールしなければなりません。
全てのconstructorを持つReactコンポーネントクラスは、super(props)のコールから始めます。

次のようにSquareのrenderメソッドを変更したら、クリックすると現在のstateが表示されるようになるはずです。

- `<button>`タグ内の`this.props.value`を`this.state.value`に変更する。
- `() => alert()`イベントハンドラを`() => this.setState({value: 'X'})`にする。
- 可読性のため`className`と`onClick`の記述を違う行にする。

これらの変更が済んだら、以下のようにSquareのrenderメソッドが`<button>`タグを返すようになるでしょう。

```
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button
        className="square"
        onClick={() => this.setState({value: 'X'})}
      >
        {this.state.value}
      </button>
    );
  }
}
```

SquareのrenderメソッドにあるonClickハンドラによりthis.setStateがコールされることで、いつでもボタンがクリックされるとReactがレンダリングを行うよう指示します。
更新後、Squareのthis.state.valueはXとなり、Xがゲームボード上に現れます。
どれでもSquareをクリックすると、そこにXが表示されます。

コンポーネントのsetStateをコールすると、Reactは自動的に子コンポーネントも更新します。

[この時点でのコード](https://codepen.io/gaearon/pen/VbbVLg?editors=0010)

### 開発ツール / Developer Tools

[Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)と[Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)向けの開発者ツールは、あなたのブラウザのデベロッパーツールでReactコンポーネントの検査をしてくれます。

<img width="300" alt="DOM developer view." src="https://reactjs.org/static/devtools-878d91461c78d8f238e116477dfe0b46-6ca3b.png">

The React DevTools let you check the props and the state of your React components.
React開発ツールではReactコンポーネントのpropsとstateを確認できます。

インストールしたら、ページ上の要素上で右クリックをして、”Inspect”をクリックし、開発者ツールを開いてください。
Reactタブが最後のタブの右に現れます。

**いくつかの手順を踏むことでCodePenと一緒に動くようになる**

- ログインまたは登録し、メールを確認する。（スパムを防ぐため）
- “Fork”ボタンをクリックする。
- “Change View”をクリックし、“Debug mode”を選択する。
- 新規タブを開くと、開発者ツールにReactタブが表示されている。

## ゲームを完成させよう / Completing the Game

これでtic-tac-gameの基礎的なブロック構成ができました。
完成させるためには、”X”と”O”を交互にボード上に置くようにし、勝者を決定する必要があります。

### 状態を移譲する / Lifting State Up

各Squareコンポーネントはゲームの状態を維持しています。
勝者をチェックするには、一箇所で9個のSquareの値を参照しなければなりません。

Boardが各Squareにそのstateを聞いて回れば良いと考えるかもしれません。
その方法はReactでも可能ですが、残念な方法です。コードは難しく理解しにくくなり、バグを産みやすく、リファクタリングを困難にします。
そうではなく、親であるBoardコンポーネントが各Squareコンポーネントの代わりにゲームの状態を持つのです。
Boardコンポーネントは各Squareコンポーネントにpropを受け渡すことで、何を表示すべきか伝えることができます。そう、先ほど数値を各Squareに受け渡したようにです。

**子コンポーネント群からデータを集める、または子コンポーネント同士でコミュニケーションするとき、あなたは共有するstateを親コンポーネントに定義する必要に迫られるでしょう。**
**親コンポーネントはstateをpropsを使って子に元通りパスできます。それによって子同士、または親子コンポーネントの間で同期を行います。**

Reactコンポーネントをリファクタし、親コンポーネントにstateを持ち上げることは一般的です。この機会にそれを試してみましょう。
Boardコンポーネントにconstructorを追加し、Boardの初期stateに9個のnullが含まれる配列を宣言しましょう。
この9nullが9squareに対応します。

```
constructor(props) {
  super(props);
  this.state = {
    squares: Array(9).fill(null),
  };
}
```

修正後にボードを埋めると、下記のような感じになるはずです。

```
[
  'O', null, 'X',
  'X', 'X', 'O',
  'O', null, null,
]
```

BoardのrenderSquareメソッドは以下のようになっているはずです

```
renderSquare(i) {
  return <Square value={i} />;
}
```

はじめに、Boardから0~8番のSquareに向けて値を受け渡しています。
別の以前のステップでは、各Squareに定義された固有のstateを、”X”に置換していました。
これはSquareはBoardから渡された値を無視しているためです。

我々は再度、propを受け渡す方法を使用します。
Boardを各Squareに、現在の値を'X'か'O'かnullだと命令するよう編集します。
先ほどBoardのconstructorで定義したsquares配列から値を読み取るよう、renderSquareメソッドを編集しましょう。

```
renderSquare(i) {
  return <Square value={this.state.squares[i]} />;
}
```

[現時点での全コードはこちら](https://codepen.io/gaearon/pen/gWWQPY?editors=0010)

各Squareは'X'か'O'かnullのいずれかのprop値を受け取ります。

次に、Squareがクリックされた時にその変更をする必要があります。
Boardコンポーネントは現在、squaresを埋めている値を持っています。
SquareがBoardのstateを変更する手段を用意しなければなりません。
もちろんstateはcomponentごとにprivateに定義されているため、SquareからBoardのstate値を直接変更することはできません。

Boardのstateをprivateに保つため、BoardからSquareに関数を渡します。
その関数はSquareがクリックされた時に呼び出される想定です。
BoardのrenderSquareを以下のように変更します。

```
renderSquare(i) {
  return (
    <Square
      value={this.state.squares[i]}
      onClick={() => this.handleClick(i)}
    />
  );
}
```

>Note
我々は返却する要素を可読性のために複数行に分割し、JavaScriptがreturnの後にセミコロンを挿入しないように括弧を追加しました。

これでBoardからSquareに、valueとonClickの2個のpropsが受け渡されるようになりました。
onClickはSquareがクリックされた時にコールできる関数です。
これからSquareに以下の変更を加えていきます。

- renderメソッドの`this.state.value`を`this.props.value`に変更します。
- renderメソッドの`this.setState()`を`this.props.onClick`に変更します。
- constructorを削除します。もうゲームの状態を管理することはありません。

これらの変更を終えて、Squareコンポーネントは以下のようになります。

```
class Square extends React.Component {
  render() {
    return (
      <button
        className="square"
        onClick={() => this.props.onClick()}
      >
        {this.props.value}
      </button>
    );
  }
}
```

Squareがクリックされると、Boardから渡されたonClickメソッドが実行されます。
これがどのように達成されたかおさらいしてみましょう。

1. `<button>`DOMコンポーネントの`onClick`propが、Reactにクリックイベントリスナーの設定をさせた。
2.  ボタンがクリックされると、ReactがSquareの`render()`メソッドに定義された`onClick`イベントハンドラをコールする。
3. イベントハンドラが`this.props.onClick`をコールし、Squareの`onClick`propがBoardによって設定された。
4. BoardはSquareに`onClick={() => this.handleClick(i)}`を受け渡し、Squareは`this.handleClick(i)`がクリックされた時にそれを実行した。
5. `handleClick()`メソッドを定義していなかったため、クラッシュした。

>Note
要素を複数行に分解して記述しているのは、可読性のためと、JavaScriptが括弧をreturnの後ろに挿入しないようにするためです。

Squareをクリックすると、エラーが発生するでしょう。まだhandleClickを定義していないためです。
これからhandleClickを追加していきます。

```
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = 'X';
    this.setState({squares: squares});
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = 'Next player: X';

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

[現時点での全コードはこちら](https://codepen.io/gaearon/pen/ybbQJX?editors=0010)

これらの変更が終わると、再びSquareをクリックし、空白を埋められるようになります。
状態は各SquareではなくBoardコンポーネントに保持されています。
Boardのstateを変更すれば、Squareコンポーネントは自動的にレンダリングします。
Boardで全ての状態を管理することで、我々は勝者を決めることができるようになりました。

Squareコンポーネントが状態を管理しないようになり、それはBoardから値を受け取り、クリックされた時にBoardに通知を送るようになりました。
React用語で、このようなSquareコンポーネントのことを **管理されたコンポーネント（controlled components）** と呼びます。Boardが完全に彼らをコントロールしています。

handleClickの処理の中で、既存のsquares配列ではなく、`.slice()`を実行してsquares配列のコピーを作成していることに注意しておいてください。
次のセクションでその理由を説明します。

### 不変性の重要さ / Why Immutability Is Important

先ほどのコードで、`.slice()`を使用してsquares配列のコピーを作成し、既存の配列を編集する代わりにコピーを編集しました。
これから、不変性についてと、その重要性について学んでいきます。

一般的に、データを変更するには二つの方法があります。
一つは、データの値を直接変更すること。もう一つは、変更を加えた新しいコピーで置き換えることです。


#### データを直接変更する / Data Change with Mutation
```
var player = {score: 1, name: 'Jeff'};
player.score = 2;
// Now player is {score: 2, name: 'Jeff'}
```

#### データを直接でなく変更する / Data Change without Mutation
```
var player = {score: 1, name: 'Jeff'};

var newPlayer = Object.assign({}, player, {score: 2});
// Now player is unchanged, but newPlayer is {score: 2, name: 'Jeff'}

// Or if you are using object spread syntax proposal, you can write:
// var newPlayer = {...player, score: 2};
```

この二つは結果は同じですが、データを直接でない方法で変更することで、次に説明するいくつかの利点を享受することができます。

#### 複雑な機能をシンプルに / Complex Features Become Simple
不変性により、複雑な機能を実装するのがとても容易になります。
この後、私達はtic-tac-gameに、以前の状態へと履歴から遡ることができる「時間遡行」機能を実装します。
この機能はゲーム特有のものではなく、UndoやRedoといった一般的なアプリケーションにも実装されている機能です。
直接のデータ変更を避けることで、以前のゲームの状態を保存しておき、後で再利用することができます。


#### 変更の検出 / Detecting Changes
直接変更される場合、変更可能なオブジェクトの変更を検知することは困難です。
検知には変更可能なオブジェクトを、それ自身と、オブジェクトツリー全体を以前の状態のコピーと比較する必要があります。

不変なオブジェクトの変更を検知するのは簡単です。
参照される不変オブジェクトが直前のものと異なる場合、それは変更されています。


#### いつReactのレンダリングが発生するかを決定できる / Determining When to Re-render in React
不変性による最も大きなメリットは、あなたが純粋なコンポーネントを作成することを助けてくれることです。
不変なデータは、それに変更があった時に、いつコンポーネントがレンダリングを実行するかを容易に決定できます。

もし`shouldComponentUpdate()`についてもっと詳しく知りたければ、そして純粋なコンポーネントを作成する方法を知りたければ、こちらの[パフォーマンスの最適化](https://reactjs.org/docs/optimizing-performance.html#examples)を読んでみてください。

### 関数コンポーネント / Function Components

Squareを関数コンポーネントにしていきます。

Reactにおいて、関数コンポーネントはrenderメソッドのみを持ち、stateを持たないコンポーネントを記述するシンプルな方法です。
クラスを定義する代わりに、受け渡されるpropsをレンダリングする関数を記述できます。
関数コンポーネントはクラスを記述するのに比べて退屈しません。そして多くのコンポーネントは関数で記述できます。

Squareクラスを以下のようなメソッドに置換していきます。

```
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```
`this.props`を`props`に変更しています。

**[現時点での全コード](https://codepen.io/gaearon/pen/QvvJOv?editors=0010)**

>Note
Squareを関数コンポーネントに置換するにあたり、`onClick={() => this.props.onClick()}`を、短く`onClick={props.onClick}`に変更しました。
クラスでは値にアクセスするのにアロー関数を使用しましたが、関数コンポーネントではその必要はありません。

### ターンを取得する / Taking Turns

そろそろ我々のtic-tac-toeゲームの、"O"がボード上にマークできないという、明らかな欠陥を修正しましょう。

初手はデフォルトで"X"になります。Boardコンポーネントのコンストラクタでstateを初期化することで、このデフォルト値を変更できます。

```
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }
```
プレイヤーが動くたびに、`xIsNext` (a boolean) の値を反転させ、次のプレイヤーを決定し、ゲームの状態を保存します。
Boardの`handleClick` 関数を、`xIsNext`変数を反転させるように修正しましょう。

```
  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```
この変更で、"X"と"O"が交互に使用されます。
それでは、Boardのレンダリングで、次のプレイヤーを表示するよう修正してみましょう。

```
  render() {
    const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      // the rest has not changed
```
この変更を行うと、以下のようなBoardコンポーネントになっているはずです。
```
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```
**[現時点での全コード](https://codepen.io/gaearon/pen/KmmrBy?editors=0010)**

### 勝者を定義する / Declaring a Winner

次のターンのプレイヤーが誰かを表示できるようになったので、次はゲームが終了したら勝者を表示するようにしましょう。
このヘルパー関数をファイル末尾に追加することで、勝者を決定することができます。

```
function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

`calculateWinner(squares)`関数は、Boardのrender関数の中でプレイヤーが勝利したかチェックするためにコールします。
プレイヤーが勝利していたら、その文章を表示します。
以下のコードでBoardのrender関数内のstatus定義を置換します。

```
  render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      // the rest has not changed
```

どちらかがゲームに勝利済みか、Squareが既に埋められている場合、`handleClick`関数をclickを無視して早期にreturnするように変更しましょう。

```
  handleClick(i) {
    const squares = this.state.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```
**[現時点での全コード](https://codepen.io/gaearon/pen/LyyXgK?editors=0010)**

おめでとうございます！
tic-tac-gameが遂に動作するようになりました。
そしてReactの基礎を習得しました。
そう、あなたは恐らく本当の勝者です。

## 時間遡行機能を追加する / Adding Time Travel

最後の練習です。
「時間遡行」で過去の手の状態に戻れるようにしましょう。

### 動作の履歴を記録する / Storing a History of Moves

squares配列に変更を加えるなら、時間遡行機能の実装は非常に困難でしょう。

しかし、一手毎に`slice()`を使用してsquares配列のコピーを生成し、不変として扱えばどうでしょう。
全ての過去のバージョンのsquares配列の状態を保持することが可能です。更に、その状態へと導くこともできます。

historyという名前の配列に、過去のsquares配列の状態を保持しましょう。
history配列は初手から最終手までの全ボードの状態を表し、以下のような形式になります。

```
history = [
  // Before first move
  {
    squares: [
      null, null, null,
      null, null, null,
      null, null, null,
    ]
  },
  // After first move
  {
    squares: [
      null, null, null,
      null, 'X', null,
      null, null, null,
    ]
  },
  // After second move
  {
    squares: [
      null, null, null,
      null, 'X', null,
      null, null, 'O',
    ]
  },
  // ...
]
```
それでは、どのコンポーネントがhistoryを保持するのかを決めていきましょう。

### 再び、状態を移譲する / Lifting State Up, Again

トップレベルのGameコンポーネントに過去の動きのリストを表示したいと思います。
表示にはhistoryにアクセスする必要があるため、historyはGameコンポーネントに配置します。

historyをGameコンポーネントに配置するにあたり、squaresを子のBoardコンポーネントから取り除きます。
「状態を移譲する / Lifting State Up」の時のように、BoardコンポーネントからGameコンポーネントに移譲を行います。
これにより、GameコンポーネントにBoardデータの全コントロールを与えることになり、Gameからhistoryの状態をレンダリングするようBoardに命令することになります。

最初に、Gameコンポーネントでstateの初期化を設定します。

```
class Game extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      history: [{
        squares: Array(9).fill(null),
      }],
      xIsNext: true,
    };
  }

  render() {
    return (
      <div className="game">
        <div className="game-board">
          <Board />
        </div>
        <div className="game-info">
          <div>{/* status */}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
}
```

次に、GameコンポーネントのonClick propsとsquaresをBoardコンポーネントに渡します。
今は各Squareに単一のclickハンドラがありますが、今後はどのSquareがクリックされたかを特定するための情報をonClickハンドラに渡す必要があります。
次の手順にしたがってBoardコンポーネントを編集していきましょう。

- Boardのコンストラクタを削除
- BoardのrenderSquareメソッドにある`this.state.squares[i]`を`this.props.squares[i]`に置き換える。
- BoardのrenderSquareメソッドにある`this.handleClick(i)`を`this.props.onClick(i)`に置き換える。

現在、Boardコンポーネントは以下のようになっているはずです。

```
class Board extends React.Component {
  handleClick(i) {
    const squares = this.state.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.props.squares[i]}
        onClick={() => this.props.onClick(i)}
      />
    );
  }

  render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

Gameコンポーネントのrender関数を、最新のhistoryを使用して表示を行うように修正していきます。

```
  render() {
    const history = this.state.history;
    const current = history[history.length - 1];
    const winner = calculateWinner(current.squares);

    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div className="game">
        <div className="game-board">
          <Board
            squares={current.squares}
            onClick={(i) => this.handleClick(i)}
          />

        </div>
        <div className="game-info">
          <div>{status}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
```

Gameコンポーネントはゲームの状態をレンダリングするようになったので、Boardのrenderメソッドから対応するコードを削除することができます。
修正が終わると、Boardのrender関数は以下のようになっているはずです。

```
  render() {
    return (
      <div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
```

最後に、handleClickメソッドをBoardからGameコンポーネントに移す必要があります。
Gameコンポーネントの仕組みが異なるため、handleClickを編集しましょう。
GameでのhandleClickメソッドは、新しいhistoryをhistoryに連結していきます。

```
  handleClick(i) {
    const history = this.state.history;
    const current = history[history.length - 1];
    const squares = current.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      history: history.concat([{
        squares: squares,
      }]),
      xIsNext: !this.state.xIsNext,
    });
  }
  ```

>Note
あなたが慣れ親しんでいるであろう配列のpush()メソッドと違い、concat()メソッドは元の配列を変更しないため、こちらを使用しています。

この時点で、BoardコンポーネントはrenderSquareとrenderメソッドのみを必要としています。
ゲームの状態とhandleClickメソッドはGameコンポーネントにあります。

**[現時点での全コード](https://codepen.io/gaearon/pen/EmmOqJ?editors=0010)**

### 過去の動作を表示する / Showing the Past Moves

tic-tac-toeゲームのhistoryを記録しているので、プレイヤーにこれまでの手の一覧を表示することができます。

React要素はファーストクラスのJavaScriptオブジェクトであることを、我々は学びました。
私たちはアプリケーションの中でそれらを受け渡すことができます。
React要素の配列を使用することで、複数のアイテムをレンダリングすることができます。

JavaScriptにおいて、全ての配列はおしなべて配列のデータをマッピングするための`map()`メソッドを所持しています。
例えば以下のように動作します。

```
const numbers = [1, 2, 3];
const doubled = numbers.map(x => x * 2); // [2, 4, 6]
```

mapメソッドを使用して、history配列を画面上でボタンとして表示されるReact要素にマッピングし、画面に表示して、クリックすると過去の状態に「ジャンプ」するようにしましょう。

ではhistoryを、Gameのrenderメソッドでマッピングしてみましょう。

```
  render() {
    const history = this.state.history;
    const current = history[history.length - 1];
    const winner = calculateWinner(current.squares);

    const moves = history.map((step, move) => {
      const desc = move ?
        'Go to move #' + move :
        'Go to game start';
      return (
        <li>
          <button onClick={() => this.jumpTo(move)}>{desc}</button>
        </li>
      );
    });

    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div className="game">
        <div className="game-board">
          <Board
            squares={current.squares}
            onClick={(i) => this.handleClick(i)}
          />
        </div>
        <div className="game-info">
          <div>{status}</div>
          <ol>{moves}</ol>
        </div>
      </div>
    );
  }
```

**[現時点での全コード](https://codepen.io/gaearon/pen/EmmGEa?editors=0010)**

tic-tac-gameの手の履歴１つ１つから、`<button>`を含む`<li>`アイテムを作成します。
ボタンは`onClick`ハンドラを持ち、ハンドラは`this.jumpTo()`をコールします。
まだ`jumpTo()`メソッドは実装していません。
今の所、ゲーム上で起きた手の一覧を見ることができ、developerツールのコンソール常に以下の警告が出るようになっているはずです。

>Warning: Each child in an array or iterator should have a unique “key” prop. Check the render method of “Game”.

上の警告が意味するところについて、これから論じていきます。

### Keyの選定 / Picking a Key

リストをレンダリングすると、Reactはレンダリングされた各リスト項目に関する情報を保持します。
リストが更新されると、Reactは何が変更されたかを判断する必要があります。
We could have added, removed, re-arranged, or updated the list’s items.
私達はリスト項目を、追加、削除、並び替え、更新を行うことができます。

以下のコードを移行することを想像してみてください。

```
<li>Alexa: 7 tasks left</li>
<li>Ben: 5 tasks left</li>
```

これを、下記のようにします。

```
<li>Ben: 9 tasks left</li>
<li>Claudia: 8 tasks left</li>
<li>Alexa: 5 tasks left</li>
```

数値の更新にに加えて、人の読解ではAlexaとBenの順序を入れ替え、Claudiaを間に挿入したように見えるでしょう。
しかし、Reactはコンピュータープログラムであり、我々の意図を知ることはありません。
Reactは意図を知ることがないため、我々は各リスト項目を区別するため、各々に異なるキープロパティを指定する必要があります。
例えば、alexa、ben、claudiaの文字列を使うことができます。
仮にこれらがデータベースのデータなのであれば、それらのIDをキーに指定しても良いでしょう。

```
<li key={user.id}>{user.name}: {user.taskCount} tasks left</li>
```

`key`は特別な、予約されたプロパティです。（`ref`と共に、より高度な機能として。）
要素が生成されると、Reactはkeyプロパティを抽出し、返却する要素の中に直接keyを保持します。
keyがpropsに属しているように見えるかもしれませんが、`this.props.key`で参照することはできません。
Reactはkeyを使用して、自動的に更新するコンポーネントを決定します。
コンポーネントはkeyについて問い合わせることはできません。

リストが再レンダリングされると、Reactは各リスト項目のkeyを取得し、直前のリストと一致するkeyを検索します。
直前のリストに存在しないkeyがある場合、Reactは新しくコンポーネントを生成します。
現在のリストにないkeyが直前のリストにある場合、Reactはそのコンポーネントを破棄します。
keyが一致すると、コンポーネントが移動します。keyは、Reactに各コンポーネントの一意性を教え、再レンダリングの間に状態を維持することを可能とします。
コンポーネントのkeyが変更された場合、コンポーネントは破棄され再生成されます。

**動的なリストを生成するたびに、適切なkeyを割り当てることを強く推奨します。**
適切なキーがない場合は、データの構成を見直すべきでしょう。

keyを指定しない場合、Reactは警告を表示した上で、配列のインデックスをデフォルトのkeyとして使用します。
配列のインデックスをkeyとして使用すると、配列の並び替え、挿入、削除などを行う際に問題になります。
明示的に`key={i}`を渡すことで警告を消すことはできますが、同様の問題があるため非推奨です。

keyはグローバルにユニークである必要はありません。
keysはコンポーネントと、その兄弟の間でユニークである必要があります。

### 時間遡行を実装する / Implementing Time Travel

tic-tac-gameのhistoryでは、過去の手には固有のIDとして、連続する番号が与えられています。
これらは並び替えられたり、削除されたり、途中に新しくデータが挿入されることはないため、これを使用しても問題ありません。

Gameのrenderメソッドで、`<li key={move}>`としてkeyを追加し、Reactのkeysに関する警告を消し去ります。

```
    const moves = history.map((step, move) => {
      const desc = move ?
        'Go to move #' + move :
        'Go to game start';
      return (
        <li key={move}>
          <button onClick={() => this.jumpTo(move)}>{desc}</button>
        </li>
      );
    });
```

**[現時点での全コード](https://codepen.io/gaearon/pen/PmmXRE?editors=0010)**

jumpToメソッドをまだ定義していないので、リスト項目をクリックすると、エラーが表示されます。
jumpToメソッドを実装する前に、stepNumberをGameコンポーネントのstateに追加して、現在表示しているステップを示します。

まず、`stepNumber: 0`をGameのコンストラクタで定義します。

```
class Game extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      history: [{
        squares: Array(9).fill(null),
      }],
      stepNumber: 0,
      xIsNext: true,
    };
  }
```

Next, we’ll define the jumpTo method in Game to update that stepNumber.
次にjumpToメソッドを定義し、そこでstepNumberを更新させます。
更に、stepNumberが偶数である場合は、xIsNextをtrueに設定します。

```
  handleClick(i) {
    // this method has not changed
  }

  jumpTo(step) {
    this.setState({
      stepNumber: step,
      xIsNext: (step % 2) === 0,
    });
  }

  render() {
    // this method has not changed
  }
```

squareをクリックした時に発火する、Gameの`handleClick`メソッドを少し変更しましょう。

The stepNumber state we’ve added reflects the move displayed to the user now.
追加したstepNumberは、ユーザーに表示している動作を反映します。
新しい手を打つと、`this.setState`の引数の一部である`history.length`の追加によって、stepNumberを更新する必要があります。
これにより、新しい手が打たれた後でも、同じ動作を表示することができます。

`this.state.history` を `this.state.history.slice(0, this.state.stepNumber + 1)` に置き換えます。
もし「時間遡行」を行ってその時点から新しい動きをするのであれば、確実にそれより未来のhistoryを破棄するようにします。

```
  handleClick(i) {
    const history = this.state.history.slice(0, this.state.stepNumber + 1);
    const current = history[history.length - 1];
    const squares = current.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      history: history.concat([{
        squares: squares
      }]),
      stepNumber: history.length,
      xIsNext: !this.state.xIsNext,
    });
  }
```

最後に、Gameコンポーネントのrenderメソッドを、常に最後の動作をレンダリングする処理から、現在洗濯されているstepNumberの状態を表示する処理になるよう変更します。

```
  render() {
    const history = this.state.history;
    const current = history[this.state.stepNumber];
    const winner = calculateWinner(current.squares);

    // the rest has not changed
```

ゲーム履歴のステップがクリックされると、tic-tac-gameのボードが即座に更新され、その時点でのボードが表示される必要があります。

**[現時点での全コード](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**

### ラッピング / Wrapping Up
