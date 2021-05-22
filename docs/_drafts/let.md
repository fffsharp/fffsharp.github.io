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
F# では基本的に変数の値を一度決めたら変えられない **束縛** を利用します。  
この束縛を行ううえで **let** というキーワードを使うので **let束縛** とも呼ばれます。  

<br>  

他の命令型のプログラミング言語を使ったことがある方は **代入** をすることで変数の中身を意図的に変更したことがあると思います。基本的にはlet束縛をした変数にそのような操作はできません。  
このような制約は命令型プログラミングに慣れ親しんだ人からすると非常に重たい制約に感じると思います。  
なぜなら、すべての変数を定数として扱っているのと変わらないためです。  

<br>  


