---
layout: post
title: "F# Scriptで開発をはじめる"
date: 2021-04-08 16:00:00 +0900
image: "https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/common/fs-octcat.png"
categories: [posts]
tags: [intro]
---

## はじめに  

F# で開発する上で作成したものを `.exe` などの実行形式にする方法と、テキストファイルのまま実行させる方法があります。  
今回はテキストファイルのまま実行させる方法を紹介していきます。  

<br>

もしみなさんが Python や バッチファイルを書いたことがあるようであれば想像しやすいと思います。  
通常、プログラムはテキストファイルをコンピュータが理解できる形にする（= コンパイル）必要があります。  
F# の場合 **事前にコンパイルしておく** こともできますし、**実行時にコンパイルしながら実行させる** こともできます。  
F# Script は **実行時にコンパイルしながら実行する方法** です。  

<br>

F# Script は大きなプログラムや速度が重視されるような場面での利用は難しいですが、業務の自動化や簡単なツールの作成などをするには適しています。  
また、事前にコンパイルする必要がないためすぐに動作の確認などができる点が優れているため、F# を入門するさいに利用するのも良いでしょう。  

<br>

## F# Script を使ってみる  

### 開発の準備をする  

プログラムは `プロジェクト` と言う管理単位で開発していくことが多いです。  
今回はどこか適当な場所に `hello-world` というディレクトリを作成して、そこをプロジェクトの保存場所とします。  
サンプルでは `C:/project/hello-world` にディレクトリを作成しています。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/dir.png)  

<br>

ディレクトリを作成したら、ここで VSCode を起動します。  
エクスプローラで右クリックをすると VSCode で開くためのオプションがあるので、それを選択すれば VSCode が起動します。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/launch-vscode.png)  

<br>

もしくターミナルで以下のように実行することで起動させることも可能です。  

{% highlight powershell %}code "C:/project/hello-world"  
{% endhighlight %}  

<br>  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/vscode-1.png)  

<br>

VSCode が起動したら `main.fsx` という名前のファイルを追加します。  
ここで重要なのは `.fsx` という拡張子です。F# Script では `.fsx` を利用しているので間違わないようにしましょう。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/vscode-2.png)  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/vscode-3.png)  

<br>

これでひとまず開発するための事前準備が完了しました。  
あとはこの `main.fsx` にコードを記述していくだけです！  

<br>
<br>

### Hello, World!!  

まずはどんなプログラミング言語を利用していても必ず一度は行う Hello, World!! の出力儀式を行ってみましょう。  
`main.fsx` に以下のコードを記述します。  

{% highlight fsharp %}printfn "Hello, World!!"  
{% endhighlight %}  

記述している途中で以下のように入力の候補が表示されたかと思います。  
これは **[開発環境の構築](https://tatsuya-midorikawa.github.io/fsdoc-jp/posts/2021/04/08/build-a-dev-env.html)** で紹介した `ionide` の機能によるものです。このように VSCode などの高機能なテキストエディタはメモ帳などとは異なり開発を補助する強力な機能を提供してくれます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/vscode-4.png)  

<br>

コードを記述し終えたら右上にある再生ボタンをクリックしてみましょう。  
そうすると今のコードが実行されて、ターミナルに `Hello, World!!` が出力されます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/vscode-5.png)  
![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/vscode-6.png)  

<br>

もしくはターミナルから直接実行させることもできます。  
その場合はプロジェクトのディレクトリに `cd` コマンドで移動してから以下のコマンドを実行します。  

{% highlight powershell %}cd C:/project/hello-world  
dotnet fsi main.fsx  
{% endhighlight %}  

<br>
<br>

### **`#load`**

少し複雑なプログラムを作成しようとすると複数のファイルにコードを分割したくなってきます。  
これは似たような機能ごとにファイルをまとめておくことで保守しやすくするために重要なことです。  

<br>  

そこで問題になってくるのは分割したファイルに書いてあるコードをどうやって呼び出すのか？ということです。  
その際に利用するのが `#load` です。  

<br>

今回は `tool.fsx` と言うファイルを作成してみて、それを `main.fsx` から利用してみましょう。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/load-1.png)  

<br>

`tool.fsx` には `add` という簡単な関数を1つだけ用意しておきます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/load-2.png)  

<br>

この `add` を `main.fsx` で利用してみます。  
まずは `main.fsx` の先頭で `#load` を利用して `tool.fsx` を指定します。  
今回は `main.fsx` と `tool.fsx` を同じディレクトリ階層に存在しているので、  

{% highlight fsharp %}#load "tool.fsx"
{% endhighlight %}  

で良いのですが、もし仮に `tool.fsx` が `modules` ディレクトリ内にあった場合は以下のように指定する必要があります。  

{% highlight fsharp %}#load "./modules/tool.fsx"
{% endhighlight %}  

そして忘れてはいけないのが `open` の行です。  
今回は `tool.fsx` というファイル名なので、その先頭を大文字にした名前で open してあげます。  
そうすることで `add` を利用することができるようになります。  
もしも `open` をしない場合は `Tool.add` とすることで利用することもできます。

<br>

`tool.fsx` を利用する準備ができたので、実際に `add` を利用してみます。  
`main.fsx` を以下のようにしてみましょう。

{% highlight fsharp %}#load "tool.fsx"
open Tool

let sum = add 10 20  
printfn $"add 10 20 = {sum}"  
{% endhighlight %}  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/load-3.png)  

<br>

これを実行すると以下のようにターミナルに結果が出力されると思います。

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/load-4.png)  

<br>

このように `#load` を利用することで分割したファイルの機能を呼び出すことができるようになります。  
もし1ファイルが大きくなってきてしまったらファイルを分割して `#load` で呼び出すことを検討してみましょう。  

<br>
<br>

### **`#r`**  

F# は **[nuget.org](https://www.nuget.org/)** などで公開されている便利な機能をまとめたライブラリを利用することができます。  
それらを利用したい場合に `#r` を利用します。  
今回は最速の json シリアライザとして有名な `Utf8Json` をサンプルに利用してみたいと思います。  

<br>

nuget パッケージを利用する場合には `#r "nuget: パッケージ名"` という書式で指定してあげます。  
Utf8Json を利用する場合には以下のように指定してあげます。  

{% highlight fsharp %}#r "nuget: Utf8Json"
{% endhighlight %}  

これで `Utf8Json` を利用する準備ができました。  
記述してから少しすると読み込みが完了すると入力補助も有効化されます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/r-1.png)  

<br>

それでは実際に以下のようなコードで nuget.org から取得した Utf8Json を利用してみましょう。  

{% highlight fsharp %}#r "nuget: Utf8Json"
open Utf8Json

type Record = {
    Name: string
    Age: int
}

let json = """
{
    "Name" : "midoliy",
    "Age" : 31 
}
"""

let value = JsonSerializer.Deserialize<Record> json
printfn $"{value}"
{% endhighlight %}  

<br>

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-script/r-2.png)  

<br>  

このように nuget.org などで公開されている膨大な数のライブラリを F# から簡単に利用できることが確認できました。  
Excel の操作をするためのライブラリやブラウザを操作するためのライブラリなど、多種多様なライブラリがあるので自分の目的にあったものを探して使ってみましょう。  

<br>
<br>

## おわりに  

このように F# Script を利用することで簡単にプログラムを作成できることがわかりました。  
もし何か業務で自動化したいものがある方は F# Script で作ってみてはいかがでしょうか？