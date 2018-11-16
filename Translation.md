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

- renderメソッドの`state.this.value`を`this.props.value`に変更します。
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
### 関数コンポーネント / Function Components
### ターンを取得する / Taking Turns
### 勝者を定義する / Declaring a Winner
## 時間遡行機能を追加する / Adding Time Travel
### 動作の履歴を記録する / Storing a History of Moves
### 再び、状態を移譲する / Lifting State Up, Again
### 過去の動作を表示する / Showing the Past Moves
### ピッキング / Picking a Key
### 時間遡行を実装する / Implementing Time Travel
### ラッピング / Wrapping Up
