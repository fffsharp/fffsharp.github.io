---
layout: post
title: "数値を表す基本型"
date: 2021-05-03 12:00:00 +0900
image: "https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/common/fs-octcat.png"
description: F#で扱われる数値を表す基本型について紹介します。
categories: [posts]
tags: ["型"]
---

## はじめに  

数値を表す基本型には **整数** と **浮動小数点数** の2種類があります。  
整数を表す型の **整数型** は表現できる範囲の大小によってさらに細分化されます。表現できる範囲がより狭い整数型の方がメモリ使用量が少なくすむというメリットがあります。時と場合によりますが、できるかぎり無駄なメモリを消費しないように自分の目的にあった型を選択することが望ましいです。また、負の数を表現する必要があるか否かによっても利用する型を変えられます。  
小数点がつく数値を表す型の **浮動小数点数型** は表現できる範囲や精度によって細分化されています。小数点以下の数値を表現できますが、現実世界とは違い計算する上で誤差が発生する可能性があるため注意が必要です。  
数値一つとってもさまざまな型があるため、最初は覚えることに苦労するかもしれません。そのため、各項で「とりあえず最初にこれだけ使っていればOK」な型を紹介します。その表現範囲で表現しきれなくなった際に改めて利用する型について意識するようにして、徐々に適したものを選択できるようになっていきましょう。  

<br>  

## 数値型の一覧

### 整数型  

| 型 | 接尾辞 | メモリサイズ | .NET型 | 範囲 |
| :-----: | :-----: | :-----: | ----- | ----- |
| byte | uy | 1 byte | System.Byte | 0 ~ 255 |
| sbyte | y | 1 byte | System.SByte | -128 ~ 127 |
| uint16 | us | 2 byte | System.UInt16 | 0 ~ 65,535 |
| int16 | s | 2 byte | System.Int16 | -32,768 ~ 32,767 |
| uint, uint32 | u | 4 byte | System.UInt32 | 0 ~ 4,294,967,295 |
| int, int32 |  | 4 byte | System.Int32 | -2,147,483,648 ~ 2,147,483,647 |
| uint64 | UL | 8 byte | System.UInt64 | 0 ~ 18,446,744,073,709,551,615 |
| int64 | L | 8 byte | System.Int64 | -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807 |  

<br>  

整数型には8種類の基本型が存在しています。  
この8種類に加えて bigint 型を加えた9種類がデフォルトで利用可能な整数型になります。  
初学者の方がこれらの型を一度に覚えるのは大変だと思います。そのため、とりあえず **int 型** を使うようにしておき、必要に迫られたときに利用目的にあった型を再選択するようにしましょう。  

<br>  

負の数を扱わない型には基本的に **u** のサフィックス（= 接尾辞）がつきます。これは **unsigned** （= 符号なし）の頭文字である **u** から来ています。  
これらの型は「unsigned 型」と呼ぶことがあります。それとは反対の負の数も表現する型のことを「signed 型」と呼ぶこともあります。覚えておくといいでしょう。  
unsigned 型は負の数がありえないことを明示的に表明したい場合によく利用されます。また、負の数を表現しなくてもよくなったことにより同じメモリサイズの signed 型の2倍程度大きな値まで扱えるようになっています。  

<br>  

F# では数値を10進数以外の16進数・8進数・2進数で指定できます。  
**16進数** は **0x** を、**8進数** は **0o** を、**2進数** は **0b** を数値の前に指定してあげます。  

{% highlight fsharp %}let hex = 0xF2B  
let oct = 0o834L  
let bin = 0b0100y{% endhighlight %}  

<br>  

また、**_** （アンダースコア）を区切り文字として任意の箇所へ入れられます。  
これは主に桁数の大きな数値を表すときにカンマの代わりとして使うことが多いです。  

{% highlight fsharp %}let n = 1_000_000_000{% endhighlight %}  

<br>

#### bigint型

| 型 | 接尾辞 | メモリサイズ | .NET型 | 範囲 |
| :-----: | :-----: | :-----: | ----- | ----- |
| bigint | I | 可変 | System.Numerics.BigInteger | -∞ ~ +∞ |  

<br>  

基本型としては提供されていませんが、巨大な整数値を表すための型として bigint 型が提供されています。  
この型は理論上、メモリが許すかぎり無限に整数値を表現できます。そのため扱う数値が大きくなれば大きくなるほどメモリを多く消費するようになります。  
また、基本の整数型に比べて計算速度も桁違いに遅くなるため利用する場合にはその点についても考慮する必要があります。  

<br>  

### 浮動小数点数型（実数型）  

| 型 | 接尾辞 | メモリサイズ | .NET型 | 範囲 |
| :-----: | :-----: | :-----: | ----- | ----- |
| float32, single | f | 4 byte | System.Single | ±1.5 × 10-45 ~ ±3.4 × 1038 （有効桁数: 7桁） |
| float, double |  | 8 byte | System.Double | ±5.0 × 10-324 ~ ±1.7 × 10308 （有効桁数: 15桁） |
| decimal | m | 16 byte | System.Decimal | 1.0 × 10-28 ~ 7.9 × 1028 （最大有効桁数: 29桁） |  

<br>  

浮動小数点数型には3種類の基本型が存在しています。   
初学者の方がこれらの型を一度に覚えるのは大変だと思いますので、とりあえず **float 型** を使うようにしておき、必要に迫られたときに利用目的にあった型を再選択するようにしましょう。  

<br>  

float や float32 は使い勝手の上では申し分ないのですが、正確な数値計算を求められる金融系の処理には向いていません。  
これは float や float32 が内部的に2進数で表現されていることと精度が有限であることに原因があります。それが元で計算に誤差が発生してしまいます。  
そこで登場するのが **decimal 型** です。decimal 型は他の2つに比べて特殊な型となっていて、内部的に10進数となっています。  
そのため float や float32 で発生するような2進数が起因となる誤差が発生しません。  
ただ、良いことばかりではなくデメリットも当然存在しています。例えば float 型の倍のメモリが必要にも関わらず表現できる数値範囲は float 型よりも狭いです。そして計算速度についても float や float32 よりも大幅に遅いです。  
そのため金額計算等、10進数で計算しないと誤差が起こってしまい、その誤差が許されない場合を除いては使わないほうがいいでしょう。
また、2進数起因でない誤差（桁落ちや情報落ち）については decimal 型でも発生します。    

<br>  

## 算術演算  

基本の数値型には足し算や引き算などのよく使われる算術演算が標準で提供されています。  
「+」や「-」などの演算を行うための記号を **演算子** といいます。  

| 演算子 | 説明 | サンプル |
| --- | --- | --- |
| + | 加算 | 1 + 2 // = 3 |
| - | 減算 | 1 - 2 // = -1 |
| * | 乗算 | 1 * 2 // = 2 |
| / | 除算 | 4 / 2 // = 2 |
| % | 剰余算 | 7 % 3 // = 1 |

<br>  

また、浮動小数点数型にのみ **べき乗** の演算がサポートされています。  

| 演算子 | 説明 | サンプル |
| --- | --- | --- |
| ** | べき乗 | 2.0 ** 8.0 // = 256.0 |  

<br>  

もしかすると **剰余算** というものを初めて見た人もいるかもしれません。  
剰余算は「割り算の余り」を求めるための演算方法です。  
上記のサンプルでは「7 / 3 = 2...1」の「余り1」のところを計算結果として得ています。  

<br>  

組み込みで用意されている算術演算では、**左辺と右辺が同じ型** である必要があります。  
つまり以下のような演算は F# では許されません。  

{% highlight fsharp %}let a = 100    // int型
let b = 50.0   // float型  
let c = a + b  // これはダメ。int と float だと型が違うため許されない{% endhighlight %}  

<br>  

こういった場合は型を揃える処理（= 変換処理）が必要となります。  
詳しくは別の場所で紹介しますが、今回の場合は以下のようにすることで計算できるようになります。  

{% highlight fsharp %}let a = 100           // int型
let b = 50.0          // float型  
let c = a + (int b)   // bをint型に変換しているためOK{% endhighlight %}  

<br>