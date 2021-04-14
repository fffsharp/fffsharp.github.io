---
layout: post
title: "F# で開発をはじめる"
date: 2021-04-14 09:30:00 +0900
image: "https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/common/fs-octcat.png"
categories: [posts]
tags: ["環境構築"]
---

## はじめに  

F# で開発する上で作成したものを `.exe` などの実行形式にする方法と、テキストファイルのまま実行させる方法があります。  
今回は **`.exe`** や **`.dll`** を出力する場合の開発方法について紹介していきます。  

<br>

今回の方法はコーディングしたソースファイルをコンパイルする形式のものになります。  
F# はコンパイルせずとも F# Script を利用すれば実行・動作させることができます。しかし F# Script の場合、規模の大きなプログラムを実行させようとすると速度的なパフォーマンスが悪くなります。  
また、業務の要件としてプログラムの難読化が必須である場合には F# Script では対応できないため事前にコンパイルしてあげる必要があります。その他にも nuget パッケージとしてライブラリを公開したい場合などもこの方法を採用しなければなりません。  

<br>

F# Script の場合と比べて手軽さはありませんが、より多彩なニーズを満たすことができます。  
より高度なことを行いたくなった場合にはぜひこの方法でプログラムを作成してみてください。  

<br>

## F# プロジェクトで開発してみる

### プロジェクトを作成する

- ステップ 1  

**`PowerShell`** や **`zsh`** などのターミナルツールを起動して、プロジェクトを作成したいディレクトリへ移動します。 以下の例ではCドライブ直下に **`projects`** ディレクトリを作成してから移動しています。  


{% highlight powershell %}mkdir C:/projects  
cd C:/projects
{% endhighlight %}  

<br>

- ステップ 2  

**`dotnet new`** コマンドを利用してプロジェクトを作成します。  
以下の例では **`HelloWorld`** というプロジェクトを作成しています。

{% highlight powershell %}dotnet new console -lang="F#" -o="HelloWorld"
{% endhighlight %}  

<br>

- ステップ 3  

VSCode でプロジェクトを開いてみましょう。  
以下のコマンドを実行すると **`HelloWorld`** プロジェクトが VSCode で開けます。

{% highlight powershell %}code ./HelloWorld
{% endhighlight %}  

VSCode でプロジェクトを開くと **`ionide`** が読み込みを開始します。  
読み込みが完了すると自動で F# のタブに移動するので **`Program.fs`** を開くと以下のような状態になると思います。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-1.png)  

**`dotnet new`** コマンドでプロジェクトを作成するとデフォルトで Hello, World を出力するコードが記述されているので、今回はこのコードをこのまま利用していきます。  

<br>

- ステップ 4  

VSCode でデバッグする環境を構築していきます。  
少し複雑な手順が必要ですが、何度かやっていくうちに覚えてしまうと思います。  
もし忘れてしまったときはこの記事に戻ってきてください。  

<br>

まず **`Run and Debug`** タブを開いて **`Run and Debug`** ボタンをクリックします。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-2.png)  

<br>  

そうするとコマンドパレットが表示されるので **`.NET Core`** を選択します。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-3.png)  

<br>  

**`.NET Core`** を選択すると自動的に空の **`launch.json`** が作成・表示されます。  
その画面の右下に **`Add Configuration`** というボタンが表示されていると思うので、それをクリックします。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-4.png)  

<br>  

構成の選択肢が表示されるので **`.NET: Launch .NET Core Console App`** を選択します。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-5.png)  

<br>  

.NET Console を実行する構成の雛形が埋め込まれるので **`program`** の項目を自身の環境に合わせて書き換えてあげます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-6.png)  

<br>  

**`target-framework`** に指定する .NET のバージョンを調べるには、PowerShell や zsh などのターミナルで調べる必要があります。  
以下のコマンドを実行することでバージョンを確認することが可能です。  

{% highlight powershell %}dotnet --version
{% endhighlight %}  

ここで表示されるバージョンは **`X.Y.ZZZ`** かそれ以上の桁数での表現になっていると思います。  
ただ **`target-framework`** に指定する時は **`X.Y`** の部分だけなので注意が必要です。  
例えば **`5.0.202`** というバージョンが表示された場合は **`net5.0`** に、**`6.0.100`** と表示された場合は **`net6.0`** という風に指定してあげます。  

<br>  

**`project-name.dll`** の箇所には **`dotnet new`** コマンドの **`-o="XXX"`** で指定した **XXX** の部分を指定してあげます。  
今回は **`HelloWorld`** としてプロジェクトを作成したので、**`HelloWorld.dll`** となります。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-7.png)  

<br>  

次に **`console`** に **`integratedTerminal`** を、**`internalConsoleOptions`** に **`neverOpen`** を指定してあげます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-8.png)  

<br>  

これで **`launch.json`** の設定は完了です。  
次に **`tasks.json`** の設定をしていきます。  
**`Run and Debug`** タブを開いて **`再生ボタン`** をクリックします。または **`F5`** を押すだけでも同様の結果を得ることができます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-9.png)  

<br>  

するとエラーメッセージが表示されるので **`Configure Task`** を選択します。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-10.png)  

<br>  

コマンドパレットが表示されるので **`Create tasks.json file from template`** を選択します。   

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-11.png)  

<br>  

さらに選択肢が表示されるので **`.NET Core`** を選択します。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-12.png)  

<br>  

すると以下のような **`tasks.json`** が自動生成されます。  
**`launch.json`** と違い、今回はこのファイルには修正を入れないのでデフォルトのままで大丈夫です。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-13.png)  

<br>   

以上でデバッグ環境の構築は完了です。  

<br>  

- ステップ 5  

それでは　**`デバッグ実行`** を行ってみましょう。  
もう一度 **`Run and Debug`** タブを開いて **`再生ボタン`** をクリックします。または **`F5`** を押してください。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-9.png)  

<br>  

すると VSCode 内のターミナルが自動で起動しプログラムがビルドされます。エラー等がなければその後にプログラムの実行も行われます。  
無事に実行まで完了するとターミナルに結果が表示されます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-14.png)  

<br>  

次にプログラムを 1 行ずつ実行していくことができる **`ステップ実行`** をやってみましょう。  
好きな行番号の左側にマウスカーソルを持っていくと半透明な赤丸が出てくると思います。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-15.png)  

<br>  

その状態でクリックをしてあげると赤丸が行に対して付与されます。今回は 11 行目で実施しました。  
この赤丸の場所のことを **`ブレークポイント`** と言いますので、覚えておくといいと思います。  
ブレークポイントは F9 ボタンを押すことでも設定できます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-16.png)  

<br>  

この状態でデバッグ実行をしてみると、ブレークポイントでプログラムの実行が止まります。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-17.png)  

<br>  

この状態で **`F10`** を押下するか **`Step Over`** ボタンを押すと現在の行の処理が実行されて次の行に移動します。  
次の行に移動すると **`Debug and Run`** タブの **`VARIABLES`** に **`message`** 変数が追加されて、変数の中身が **`from F#`** であることを確認することができます。

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-17-1.png)  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-18.png)  

<br>  

**`F5`** か **`Continue`** ボタンを押すと次のブレークポイントの場所まで通常のように実行されます。  
今回は 1 箇所しかブレークポイントを設定していないため、プログラムの実行が完了してターミナルに処理結果が表示されます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-18-1.png)  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-20.png)  

<br>

ではもう一度その状態でデバッグ実行をしてみます。  
引き続き 11 行目で処理が止まると思います。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-17.png)  

<br>

ここで次は **`F11`** か **`Step Into`** ボタンを押してみます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-17-2.png)  

<br>  

すると今回は次の行ではなく、**`from関数`** の中へ移動しました。  
さらに VARIABLES で from 関数の引数である　**`whom`** に何が指定されているのかも確認可能です。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-19.png)  

<br>  

このように **`Step Over`** と **`Step Into`** を使い分けることで、ステップ実行で見ていきたい内容の解像度を自在に操ることができます。  

<br>

以上が簡易的ですが F# でのプロジェクトを作成して開発する方法となります。  

<br>
<br>  

### ソリューションを作成する  

大規模な開発になってくると 1 つのプロジェクトで完結することは少なくなってきます。  
これはプロジェクトを細分化することによって影響範囲を局所化できたり、変更した **`.dll`** だけを入れ替えるだけでシステムを更新できるようになったり、変更したプロジェクトだけリビルドするだけで済むためビルド時間を大幅に短縮できたりするようになったりするためです。  

<br>  

複数のプロジェクトを作成して 1 つの大きなシステムを作成する場合にはプロジェクトをバラバラに管理するよりも 1 つ所にまとめておいた方が管理しやすいです。そこで登場する管理単位が **`ソリューション`** です。  
多くの場合 **`1 システム = 1 ソリューション`** となります。  

<br>  

先に述べたようにソリューションの中には 1 つ以上のプロジェクトが属する形となります。  
F# の場合、プロジェクトは **`.fsproj`** ファイルで管理していました。  
そしてソリューションは **`.sln`** ファイルで管理します。  
ここでは **`.sln`** の作成方法について紹介していきます。  

<br>  

- ステップ 1  

まずはソリューションを管理するディレクトリと **`.sln`** を作成します。  
今回は **`C:/projects`** を作業ディレクトリとして作業していきます。  

{% highlight powershell %}cd C:/projects
{% endhighlight %}  

<br>  

**`.sln`** を作成するためには **`dotnet new sln`** コマンドを利用します。  
今回は **`HelloSystem`** というソリューションを作成しました。  

{% highlight powershell %}dotnet new sln -o="HelloSystem"
{% endhighlight %}  

<br>  

コマンドを実行すると **`HelloSystem`** というディレクトリの下に **`HelloSystem.sln`** というファイルができていることがわかります。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/sln-1.png)  

<br>  

**`HelloSystem`** ディレクトリに移動しておきます。  

{% highlight powershell %}cd HelloSystem
{% endhighlight %}  

<br>

- ステップ 2  

ソリューションに所属させるプロジェクトを作成します。  
今回はコンソールプロジェクトとライブラリプロジェクトを一つずつ作成します。  


{% highlight powershell %}dotnet new console -lang="F#" -o="HelloConsole"  
dotnet new classlib -lang="F#" -o="HelloModule"
{% endhighlight %}  

<br>  

コマンドを実行すると **`HelloSystem.sln`** と同じ階層に 2 つのプロジェクトができたと思います。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/sln-2.png)  

<br>  

- ステップ 3  

作成したプロジェクトを **`HelloSystem.sln`** に所属させます。  
**`dotnet sln add`** コマンドを利用することで簡単に所属させることが可能です。  

{% highlight powershell %}dotnet sln add ./HelloConsole  
dotnet sln add ./HelloModule
{% endhighlight %}  

<br>

コマンドを実行すると **`HelloSystem.sln`** にプロジェクトが追加されます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/sln-3.png)  

<br>  

これでソリューションの構築は完了です。  

<br>  

- おまけ  

今回作成した **`HelloConsole`** の中で **`HelloModule`** を利用したい場合、このままでは使えません。  
これを解消するには **`HelloConsole.fsproj`** に **`HelloModule`** を利用することを宣言する必要があります。  
手で書いてもいいのですが通常 **`dotnet add reference`** コマンドを利用します。  

{% highlight powershell %}cd HelloConsole  
dotnet add reference ../HelloModule
{% endhighlight %}    

<br>  

コマンドを実行すると **`HelloConsole.fsproj`** に **`HelloModule`** を利用することを表す記述が追加されます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/sln-4.png)  

<br>  

 このように特定のプロジェクトを利用することを **`.fsproj`** に追加することを **`参照を追加する`** ともいうので覚えておくと良いでしょう。  

<br>  
<br>  

## おわりに  

今回はコマンドの使い方が多い内容だったため覚える量が多かったと思います。  
この記事で紹介している内容についてはすぐに暗記して使えるようになる必要はありません。  
何度もアプリを作成していく中で勝手に手が覚えるので、それまではこの記事を参考にしつつプロジェクトを作成していきましょう。  