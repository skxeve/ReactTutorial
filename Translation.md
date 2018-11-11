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

一度でチュートリアルを完了する必要はありません。１セクションずつでも、できる速度で学習しましょう。

チュートリアルはコピペでも動くようになっていますが、手打ちで進めることを推奨します。体で覚え、深い理解を得るにはそれが一番です。

### 何を作るのか？ / What Are We Building?

インタラクティブなtic-tac-toeゲーム[^1]をReactで作ります。

最終的な結果を[こちら](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)で確認することができます。
もしコードが理解できなかったり、文法に親近感を感じなくても、心配はいりません。
チュートリアルを完了する頃には、きっとReactと文法を理解できるでしょう。

チュートリアルを続ける前に、tic-tac-toeゲームを遊んでみることをお勧めします。One of the features that you’ll notice is that there is a numbered list to the right of the game’s board. This list gives you a history of all of the moves that have occurred in the game, and is updated as the game progresses.

You can close the tic-tac-toe game once you’re familiar with it. We’ll be starting from a simpler template in this tutorial. Our next step is to set you up so that you can start building the game.

[^1]: 三目並べ

### 前提条件 / Prerequisites

We’ll assume that you have some familiarity with HTML and JavaScript, but you should be able to follow along even if you’re coming from a different programming language. We’ll also assume that you’re familiar with programming concepts like functions, objects, arrays, and to a lesser extent, classes.

If you need to review JavaScript, we recommend reading this guide. Note that we’re also using some features from ES6 — a recent version of JavaScript. In this tutorial, we’re using arrow functions, classes, let, and const statements. You can use the Babel REPL to check what ES6 code compiles to.

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


## 概要 / Overview

### What is React?

## スターターコードの検査 / Inspecting the Starter Code

### Passing Data Through Props
### Making an Interactive Component
### Developer Tools

## Completing the Game
### Lifting State Up
### 不変性の重要さ / Why Immutability Is Important
### Function Components
### Taking Turns
### Declaring a Winner
## Adding Time Travel
### Storing a History of Moves
### Lifting State Up, Again
### Showing the Past Moves
### Picking a Key
### Implementing Time Travel
### Wrapping Up
