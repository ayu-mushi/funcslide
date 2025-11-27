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
<strong>純粋</strong>な<strong>式</strong>を組み合わせてプログラミングする、
</div>
<div style="font-size: 28px;text-align: center;">
<strong>プログラミングのスタイル</strong>
</div>
</div>

---

# あれ？式ってなんだっけ？

式というのは、

* プログラムの中で、括弧でくくっても意味が変わらない部分のこと。
* 値を持つもの。
* 変数や配列の要素に代入できる
* 型がある
* `1`もそうだし、`1 + 1`とか。あとは `f(a)` とか`(x == 1) ? ok() : ng()`。
* ラムダ式 (関数が値)

文は、

* 関数呼び出しに `;` をつけたもの ( `;` がない関数呼び出しは式)
    * `func();`
* if文、while文、for文などの制御構造

手続き型プログラミングが文を並べてプログラミングするのに対し、関数型プログラミングは式でプログラミングするプログラミングスタイル

---

# 純粋な式

純粋な式は、

* 値を求める以外のことを何もしない。
* いつ実行しても同じ値になる。


---

# 不純な式

* `++i`
    * 先の条件を両方とも破っている。
    * iの値によって違う値になることがあるし、値を求めるだけではなく、代入もしている。
* `System.out.println("aaaa")`
    * 戻り値はvoidなので無く、ある意味常に同じだが、値を求める以外のこと（コンソールに出力する）をしている
* `10000 / 0`
    * 例外を投げる場合は、値を返す以外のことをしているので純粋ではない
* `rand()`
    * 実行するときによって違う値になる

「値を出すという以外に、式が行うこと」および「式の中身以外の要因に応じて値が変化すること」を副作用という(入出力、乱数、例外、代入、変数の使用はすべて副作用の例)

---

## 関数型プログラミングってなに？もういちど説明
* 純粋な式で書けるところは、なるべく純粋な式で書く
* プログラムのうち、純粋な式で書かれた部分と、副作用を使う部分は分ける。

  <div class="text-5xl font-bold mt-6 py-12 px-10">
    これが、関数型プログラミング！
  </div>



----

## 関数型プログラミングの具体例
``` typescript
    const result =
        [0, 1, 2, 3, 4].map(x => x + 1)
            .filter(x => x % 2 == 0) // 偶数のみを選別
            .reduce((x,acc) => x + "," + acc, "!") // 
```



<!--
## 例: オセロだったら…

* 純粋関数だけでできている部分
    * プレイヤーが駒をおいて、相手の駒をひっくり返す関数
        * play : (Field, Player, (int, int)) -> Field
    * ゲーム終了を判定する関数
        * isEnd : Field -> boolean
    * どちらが勝ちかを判定する関数
        * whoIsWinner : Field -> Player
* 入出力関連は別に分ける (副作用を分離)
  * クリック入力を取り、「プレイヤーが駒を置く」関数に渡す
  * さっきの関数の返り値を画面に反映させる

-->


<!-- メソッドチェーン -->

----

## 宣言型プログラミング：クイックソートで説明

手続き型の考え方：

```
int arr[n][m] ;

arrを初期化…

arrを並び替え

arrを出力
```

----

## 関数型言語
* …は、関数型プログラミングがしやすい言語
* 関数型プログラミングがしやすくなるために、以下のような機能がある:
    * 不変データ構造
        * 中身を破壊的に変更できない配列やオブジェクト
        * 前の値が残る
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
* pandoc
    * markdownやhtmlなどの文章をいろいろな形式に変換できるコマンド。Haskellで書かれてる


---

### 関数型プログラミングの利点
- 再利用性が高い
- ライブラリを作りやすい
- テストがしやすい


---
## 手続き型／命令型プログラミング
- 逐次実行
- 条件分岐
- 繰り返し処理

---

## ここでは触れなかった発展的な話題
* 代数的データ型
    * int × string や int + boolean のような型の掛け算、足し算が可能に。新しい型を作り出せる
* 無限リスト
    * 無限の長さを持つデータ構造を作る。途中までしか作られていないが、必要になると計算される。
* モナド
    * 純粋関数型言語で副作用を扱う技術。

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


## まとめ
* 関数型プログラミングは、純粋関数を使うプログラミングのスタイル
* 純粋関数以外の関数が行うことは、副作用
* 関数型プログラミングでは、副作用と、純粋関数を分離して書く



<!-- 小さいパーツから徐々に複雑なものを作る -->
