---
layout: post
title: "型推論"
date: 2023-08-15 9:00:00 +0900
image: "https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/common/fs-octcat.png"
description:
categories: [posts]
tags: ["型"]
---

## 概要

F#は強い静的型付け言語です。すなわち：

- 強い：（暗黙的型変換などによる）別の型への解釈は行わない
- 静的型付け：プログラムの実行前に型検査が行われる

ここで型検査とは、型に基づくエラーによりプログラムが異常終了することがないか検査することをいいます。

F#は静的型付け言語ですが、コード上に型を明示的に記載する必要はありません。例えば

{% highlight fsharp %}
let x = 'a'
let f a b = a + b + 100
{% endhighlight %}

と書けばよく

{% highlight fsharp %}
let x : char = 'a'
let f (a : int) (b : int) : int = a + b + 100
{% endhighlight %}

と書く必要はありません(下の記載も誤りではありません)。これはプログラマに変わって、コンパイラが自動で型を推定してくれていることによります。このことを、**型推論**といいます。F#の型推論機能は、C#よりも強力です。

## サンプル

次の例では、引数(`a`, `b`)と戻り値の型は、`int`と型推論されます。

{% highlight fsharp %}
let f a b = a + b + 100
{% endhighlight %}

ここでは、`100`の型が`int`ということから、引数と戻り値の型が型推論されています。`100`の型が`int`から、`100 + a + b`の型が`int`と推論され、`a`, `b`の型も`int`と推論されます。一般に、関数の戻り値の型は、関数に含まれている最後の式の型によって決まります。

値の使用方法のすべてを満たす単一の型が存在しない、あるいは値の使用方法に矛盾がある場合に、コンパイラはエラーを報告します。

## 自動汎化

コンパイラが型推論できない場合はあるでしょうか？ 例えば、関数のコードを検査した際、その処理が引数の型に依存していない場合があります。

{% highlight fsharp %}
let makeTuple a b = (a, b)
{% endhighlight %}

このコードは、一見して、`a`, `b`, `(a, b)`のいずれも、型を推論することは難しそうです。

このような場合、コンパイラは、引数の型をジェネリック型と認識します。F#では、上記のような一般的なコードを記載することが許されており、これは関数の汎用的な記載を許します。コンパイラが引数の型をジェネリック型と認識することを、**自動汎化**といいます。

## 参考

- [Type Inference - Microsoft Docs](https://learn.microsoft.com/en-us/dotnet/fsharp/language-reference/type-inference)
