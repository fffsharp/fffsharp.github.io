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

VSCode でプロジェクトを開いて、実行してみましょう。  
以下のコマンドを実行すると **`HelloWorld`** プロジェクトが VSCode で開けます。

```powershell
code ./HelloWorld
```


