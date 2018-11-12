# チュートリアル：React事始め

このチュートリアルでは、既存のReact知識は想定していません。

## チュートリアルを始める前に / Before We Start the Tutorial

このチュートリアルでは小さなゲームを作ります。
**ゲームを作りたいわけではないから飛ばしてしまおうと思うかもしれませんが、それでも試してみてください。**
このチュートリアルを通して習得する技術は、様々なReactアプリを作るための基礎的なものであり、マスターすることでReactについて深い理解を得られるでしょう。

*Tips*
*このチュートリアルは、手を動かして学ぶことを好む人向けに作られています。*

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

If you need to review JavaScript, we recommend reading this guide.
もしJavaScriptについて確認したいことがあるなら、[このガイド](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)を読むことをお勧めします。
また、我々はES6（JavaScriptの最近のバージョン）のいくつかの機能を使用します。
このチュートリアルでは、アロー関数、classes、let、const の文法を使用します。
(Babel REPL)[https://babeljs.io/repl/#?presets=react&code_lz=MYewdgzgLgBApgGzgWzmWBeGAeAFgRgD4AJRBEAGhgHcQAnBAEwEJsB6AwgbgChRJY_KAEMAlmDh0YWRiGABXVOgB0AczhQAokiVQAQgE8AkowAUAcjogQUcwEpeAJTjDgUACIB5ALLK6aRklTRBQ0KCohMQk6Bx4gA]を使用すれば、どのようなES6コードがコンパイルされるか確認できます。

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

The render method returns a description of what you want to see on the screen.
renderメソッドはあなたがどうレンダリングしたいかの詳細を返却します。
 React takes the description and displays the result.
Reactはそれを受け取り、その結果を表示します。
In particular, render returns a React element, which is a lightweight description of what to render.
特にrenderメソッドが返却するのは、軽量なレンダリング情報であるReact elementです。
  Most React developers use a special syntax called “JSX” which makes these structures easier to write.
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

ShoppingListコンポーネントは内包された<div />や<li />といったDOMコンポーネントを単にレンダリングするものです。
あなたは同じようにしてカスタムReactコンポーネントを作成し、レンダリングすることができます。
例えば、<ShoppingList /> と記述することで、ショッピングリストを参照することができます。
各Reactコンポーネントはカプセル化され、独立して操作できます。これがシンプルなコンポーネント群から複雑なUIを構築することを可能にしています。

### Propsを使ったデータの受け渡し / Passing Data Through Props

### 対話的なコンポーネントの作成 / Making an Interactive Component
### 開発ツール / Developer Tools

## ゲームを完成させよう / Completing the Game
### 状態を移譲する / Lifting State Up
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
