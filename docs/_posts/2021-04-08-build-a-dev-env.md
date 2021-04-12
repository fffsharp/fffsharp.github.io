---
layout: post
title: "開発環境の構築"
date: 2021-04-08 12:00:00 +0900
image: "https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/common/fs-octcat.png"
categories: [posts]
tags: [intro]
---

## はじめに  

F# で何かを開発するには必須となるツールと必須ではないけれども導入しておくと便利となるツールがあります。  
この記事では必須ツールの導入方法と Windows や Mac、Linux で利用できる開発を補助するツールの導入方法について紹介していきます。  

<br>

そもそもの話ですがプログラムを作成するさいには `ソースコード` や `ソースファイル` などと呼ばれるテキストファイルと `コンパイラ` と呼ばれるテキストファイルからコンピュータや実行環境が理解できるものに変換するソフトが必要となります。  
今回、必須ツールとして紹介する `dotnet` というツール（または実行環境）はこのコンパイラの役割を果たします。では必須ではないツールはなんなのかと言うとソースコードを作成する上で人間の補助をしてくれるツールのことを指します。  
極端な話をするとWindowsではメモ帳が、Macではテキストエディットがデフォルトでインストールされているので、`dotnet` さえ導入してしまえばすぐに開発を始められます。ただ、それでは効率の良い開発ができませんし、ソースコードの記述が苦痛を伴うものとなります。そのためソースコードを記述することに適したテキストエディタの導入をオススメしています。  

<br>  
<br>  

## 導入するツール  

### **`dotnet`**  

F# を使うには Microsoft が提供している dotnet というツールが必要です。  
このツールは [.NETの公式ダウンロードページ](https://dotnet.microsoft.com/download) からインストーラを取得することができます。  
業務上、長期のサポートが必要であったりなどの理由がなければ最新のSDKを取得するようにしましょう。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/dotnet-download.png)  

<br>
ダウンロードしたインストーラを実行すると、インストールしてもよいか聞かれるので案内にしたがってインストールを実行してください。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/installer-1.png)  
![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/installer-2.png)  
![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/installer-3.png)  

<br>
インストールが完了したらコマンドプロンプトやPowerShell、zsh、bushなどのターミナルツールを起動しましょう。  
Windowsの場合はタスクバーから検索をすることで起動することができます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/powershell.png)  

<br>
ターミナルツールを起動したら `dotnet --version` コマンドを実行します。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/dotnet-1.png)  

<br>
問題なくインストールされている場合は以下のようにdotnetツールのバージョンが表示されると思います。  
私の環境では `5.0.202` と表示されていますが、dotnetは随時更新されていますのでみなさんの環境ではより新しいバージョンになっているかもしれません。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/dotnet-2.png)  

<br>  
<br>  

### **`Visual Studio Code (VSCode)`**  

F# の開発する上では必須ではないですが導入しておくと格段に開発の効率が上がるのでインストールすることをオススメします。  
[Visual Studio Codeの公式ダウンロードページ](https://code.visualstudio.com/Download) からインストーラを取得することが可能です。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/vsc-download.png)  

<br>
ダウンロードしたインストーラを実行すると、インストールしてもよいか聞かれるので案内にしたがってインストールを実行してください。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/vsc-installer-1.png)  

<br>
ここの「PATHへの追加」にチェックを入れるようにしてください。

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/vsc-installer-2.png)  
![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/vsc-installer-3.png)  
![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/vsc-installer-4.png)  

<br>
インストールが完了したらPCを再起動してから、PowerShell などのターミナルツールを起動して `code --version` コマンドを実行してみてください。　　

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/code-1.png)  

<br>
無事 VSCode のインストールが成功している場合は VSCode のバージョンが表示されると思います。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/code-2.png)  

<br>  
<br>  

### **`ionide`** : VSCode の拡張機能  

VSCode には豊富な拡張機能が提供されています。  
`ionide` は VSCode で F# を開発するのを強力にサポートしてくれる拡張機能です。  
導入するのを忘れないようにしましょう。  

<br>

まずは VSCode を起動します。  
VSCode が起動したら拡張機能を追加していきます。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/vscode-1.png)  
  
<br>

拡張機能の検索画面が表示されたら検索ボックスに `ionide` と入力します。  
そうすると `ionide-fsharp` という拡張機能があると思いますので、`install` をクリックして導入します。  

![](https://raw.githubusercontent.com/tatsuya-midorikawa/images/main/fsdoc-jp/build-a-dev-env/vscode-2.png)  

<br>
<br>

## おわりに  

これで F# を利用していく準備ができましたので、どんどん開発をしていきましょう。  