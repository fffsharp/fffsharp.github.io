---
layout: post
title: "let束縛とは"
date: 2021-05-20 12:00:00 +0900
image: "https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/common/fs-octcat.png"
description: 
categories: [posts]
tags: ["基本"]
---

## 概要  

F# では値と名前を関連付けることを **束縛** または **バインド** といいます。この束縛を行ううえで **let** というキーワードを使うので **let束縛** とも呼ばれます。  
束縛された値は基本的に **変更できません** 。この「値を変更できない」性質を **immutable** (イミュータブル) といいます。  

<br>  

命令型のプログラミング言語を使ったことがある方は **代入** をすることで変数の中身を意図的に変更したことがあると思います。基本的にはlet束縛をした値にそのような操作はできません。  
このような制約は命令型プログラミングに慣れ親しんだ人からすると非常に重たい制約に感じることでしょう。なぜなら代入をよく使うようなプログラミングスタイルからすると、すべての変数を定数として扱っているのとなんら変わらなく感じるためです。  

<br>  

ではなぜ F# では immutable な値がメインで利用されているのでしょうか？  
これは、例えば以下のようなメリットがあるためです。  

1. 「値が入っていない」ということが発生しない  
2. 「いつのまにか値が変わっている」ということが発生しない  

<br>  

このようなメリットがあるおかげでコードの可読性や保守性を高められたり、処理の並列化がしやすなったりします。  

<br>  
<br>  

## サンプル  

let束縛は ```let 名称 = 値``` の形で宣言します。  
いくつかの例を見てみましょう。

{% highlight fsharp %}// 数値リテラル
let number = 100

// 文字列リテラル
let title = "Fun Fan F#!!"

// 関数値
let func = fun x -> x * 2
{% endhighlight %}  

難しいことは何もなく、とても簡単に let 束縛は使うことができます。  
それでは実際に let 束縛した値を計算に使ってみましょう。  

{% highlight fsharp %}// 100 を束縛
let oneHundred = 100
// 整数値を 3 倍する関数値を束縛
let triple = fun x -> 3 * x

// 実際に計算をさせてみる
let answer = triple oneHundred
// 300 が出力される
printfn $"%d{answer}"
{% endhighlight %}  

このように整数値を直接計算させた場合と遜色なく利用できます。  
また既定では、C# や Java、Python、TypeScript などで許容されている **再代入** は禁止されています。  

{% highlight fsharp %}// 100 を束縛
let oneHundred = 100
// F# では再代入は禁止されている
oneHundred <- 200
{% endhighlight %}  

<br>  
<br>  

## let mutable  

F# では基本的に値は immutable なものですが、変更可能な値 (= mutable な値) として let 束縛することもできます。その場合は **let mutable** というキーワードを利用して値を束縛します。  
これは C# や Java、Python、TypeScript などの非関数型プログラミング言語でいうところの **変数** にあたります。let mutable で束縛した場合には **再代入** が許容されます。  

（TBD）