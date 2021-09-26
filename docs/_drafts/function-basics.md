---
layout: post
title: "関数の基礎"
date: 2021-08-30 12:00:00 +0900
image: "https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/common/fs-octcat.png"
description: 
categories: [posts]
tags: ["関数"]
---

## 概要  

関数は「入力された値を別な値に変換して出力する装置」のようなものだと考えられます。  

<br>

例えば、自動販売機を考えてみます。  
自動販売機に 120 円を入れて、飲み物を選択すると飲み物が出てきます。  
ここでは「自動販売機」が関数の役割を果たしています。  

- 自動販売機 ・・・ 関数
- 選択肢 ・・・ 入力1
- 120 円 ・・・ 入力2
- 飲み物 ・・・ 出力

のような関係性です。  
このように値を変換する機能のことを関数といいます。  

<br>

F# では関数を以下のような構文で表現します。  
関数を作成 (= 定義) することを **関数宣言** とも言います。

{% highlight fsharp %}// 関数宣言  
let 関数名 引数リスト: 戻り値の型 = 処理  

//　関数を使う  
let 結果 = 関数名 引数1 引数2 ... 引数N  
{% endhighlight %}  

前述の自動販売機の例の場合、F# 上では例えば次のように表現されます。  

{% highlight fsharp %}let 自動販売 選択肢 入金額: 飲み物 =  
  if 入金額 < 120 then
    None
  else
    match 選択肢 with
    | CocaCola -> コーラ
    | GreenTea -> お茶
    | Water -> 水
    |> Some  

let drink = 自動販売 CocaCola 120
{% endhighlight %}  

<br>  

関数宣言中の **戻り値の型** は省略することも可能です。  