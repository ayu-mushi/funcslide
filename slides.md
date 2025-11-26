---
# try also 'default' to start simple
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: オブジェクト指向はもう古い？！関数型プログラミング、超入門☆
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# duration of the presentation
duration: 35min
css: styles.css
---
# オブジェクト指向はもう古い？！関数型プログラミング、超入門！


---

# 関数型プログラミング

<div style="position: absolute;top: 50%;left: 50%;transform: translate(-50%, -50%);font-size: 48px;font-weight: bold;text-align: center;">
ってなに？？
</div>

---
transition: slide-up
---

# 一言でいうと…


<div style="position: absolute;top: 50%;left: 50%;transform: translate(-50%, -50%);font-size: 48px;font-weight:normal;text-align: center;">
<div style="font-size: 28px;text-align: center;">
<strong>純粋関数</strong>を組み合わせてプログラミングするという、
</div>
<div style="font-size: 28px;text-align: center;">
<strong>プログラミングのスタイル</strong>
</div>
</div>

---

# 純粋関数とは！？！？

<ol>
<div v-click>こんな関数です：</div>
<span v-click><li>同じ引数を与えれば、必ず、いつでも、同じ返り値が返る</li></span>
<span v-click><li>引数から返り値を求める以外のことを、何もしない</li></span>
</ol>
<!--  (返り値がどうなるかは、引数以外の何ものにも依存しない) -->

<div v-click>
要は、数学で言う関数 (xが決まるとyが唯一に決まるやつ) です
</div>

```ts
function aisatsu(name : string, isMorning: boolean) : string {
    if(isMorning){
        return "おはよう、" + name + "さん！";
    } else {
        return "こんばんちわ、" + name + "さん！";
    }
}
```

<div v-click>    例： <code>aisatsu("ロバート", true)</code>というのは、何度呼び出しても、<code>"おはよう、ロバートさん！"</code>という値が返る。</div>

---
transition: slide-up
level: 2
---


## じゃあ逆に、純粋関数ではない関数って？(1)
関数の外の変数に代入したり…
```typescript  twoslash
let count : number = 0;

function helloWithCount(name: string) : string {
    count++;
    return "こんにちは、" + name + "さん";
}
```

関数外の変数を使ったり…。

```typescript  twoslash
let count;
function helloCount() : string {
    return "あなたは今日私に" + String(count) + "回こんにちはをしましたッッ！！！";
}
```
---
transition: slide-left
level: 2
---



## じゃあ逆に、純粋関数ではない関数って？(2)

入出力を行ったり…
```typescript  twoslash
function hello() : void {
    const name = prompt("名前を入力してください");
    console.log("こんにちは！！！！！！！！！！！" + name + "さん！！");
}
```

乱数を使ったり…
```typescript  twoslash
function random() : number {
    const r : number = Math.random();
    return r; // 例: 0.2348762...
}
```

----

## じゃあ逆に、純粋関数ではない関数って？(3)
* 例外を投げる
* データベースから取得、書き込み

→これらの、関数の、引数から (唯一通りの) 返り値を求める以外の振る舞いをまとめて、
  <div class="text-5xl font-bold mt-6 py-12 px-10">
  関数の副作用
  </div>

と呼ぶ！

----

## 関数型プログラミングってなに？もういっかい説明
* 純粋関数だけで書けるところは、なるべく純粋関数にする。
* プログラムのうち、純粋関数で書かれた部分と、副作用を使う部分は分ける。

  <div class="text-5xl font-bold mt-6 py-12 px-10">
    これが、関数型プログラミング！
  </div>



----

## 例: オセロだったら…

* プレイヤーからの入力（次に駒を置く場所）を、座標で表す
  * (縦軸=1, 横軸=5)
* 「次に駒を置く場所」「現在のオセロの盤面」「今黒の番か白の番か」の3つを引数として受取り、「次のオセロの盤面」「今どちらの番か」「ゲーム終了したかどうか、もししたならどちらが勝ちか」を返り値として返す、という関数を作る (純粋関数)
* 入出力関連は別に作る (副作用を分離)
  * クリック入力を取り、さきほどの関数に渡す
  * さっきの関数の返り値を画面に反映させる


----

## 高階関数

----

## 関数型言語
* …は、関数型プログラミングがしやすい言語
* 関数型プログラミングがしやすくなるために、以下のような特徴がある:
    * 不変データ構造
        * 中身を破壊的に変更できない配列やオブジェクト
    * 高階関数

* 例:
  * Haskell
    * 純粋関数型言語。型に関する機能が豊富で、自分で色々な型を作れる。楽しい。
  * Scala
    * Javaと同じでJVM上で動く。
  * Lisp
    * 動的型付きの関数型言語。括弧がいっぱい。


<!-- map とか reduce でお茶を濁す -->


---

## 関数型言語の実用例
* Jane Street
    * 関数型言語OCamlを使い、金融取引系のシステムを作っている。
* Facebook (Meta)
    * スパムフィルタリングでHaskellを使用。
* Chatwork
    * 業務用のチャットアプリ。関数型言語のScalaを利用している。
* 朝日ネット
    * インターネットサービス・プロバイダ。Haskellを利用。
* Tezos
    * OCamlで開発されたブロックチェーンプラットフォームで、Michelsonという関数型のような言語で契約（スマートコントラクト）を書ける。


---

### 関数型プログラミングの利点
- 再利用性
- 粗結合
- テストがしやすい


---
## 手続き型／命令型プログラミング
- 逐次実行
- 条件分岐
- 繰り返し処理

---

## ここでは触れなかった発展的な話題
* 代数的データ型
    * int × string や int + boolean のような型の掛け算、足し算が可能に
* 無限リスト
    * 無限の長さを持つデータ構造を作る

<!--

## 純粋関数
- **参照透過性**  
  同じ値を持つ式同士を置き換えても振る舞いが変わらない


## 不変性（イミュータブル）
- 手続き型では配列は `const` にしても中身を書き換えられる
- 関数型言語では配列やオブジェクトの中身を書き換え不可


## 関数が第一級
- 関数を引数として渡せる
- 関数を戻り値として返せる
- 関数を配列や連想配列などのデータ構造の中に入れることができる


## 副作用
- 入出力操作
- 変数への再代入
- 純粋関数は副作用を持たない

-->

## 関数型プログラミングのメリット
- 抽象化が容易
- 再利用性が高い。
- 粗結合
- 安全性が高い


---
layout: two-cols
layoutClass: gap-16
---

おわり




