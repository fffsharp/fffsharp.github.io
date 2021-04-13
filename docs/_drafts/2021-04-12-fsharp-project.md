---
layout: post
title: "F# で開発をはじめる"
date: 2021-04-10 16:00:00 +0900
image: "https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/common/fs-octcat.png"
categories: [posts]
tags: [intro]
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

```powershell
mkdir C:/projects
cd C:/projects
```

<br>

- ステップ 2  

**`dotnet new`** コマンドを利用してプロジェクトを作成します。  
以下の例では **`HelloWorld`** というプロジェクトを作成しています。

```powershell
dotnet new console -lang="F#" -o="HelloWorld"
```

<br>

- ステップ 3  

VSCode でプロジェクトを開いてみましょう。  
以下のコマンドを実行すると **`HelloWorld`** プロジェクトが VSCode で開けます。

```powershell
code ./HelloWorld
```

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

```powershell
dotnet --version
```

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

それではもう一度 **`Run and Debug`** タブを開いて **`再生ボタン`** をクリックします。または **`F5`** を押してください。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-9.png)  

<br>  

すると VSCode 内のターミナルが自動で起動しプログラムがビルドされます。エラー等がなければその後にプログラムの実行も行われます。  
無事に実行まで完了するとターミナルに結果が表示されます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/fsharp-project/vscode-14.png)  

<br>  


