---
title: "hugoで自サイト構築-Projects.yaml編"
date: 2022-07-31T16:18:00+09:00
description: hugoで自サイト構築-Projects.yaml編
menu:
  sidebar:
    name: hugoで自サイト構築-Projects.yaml編
    identifier: hugo-aboutProjects
    parent: hugo
    weight: 206
tags: ["hugo", "サイト構築"]
categories: ["hugo"]
---
  
## Projects.yamlの設定について  
このセクションは自分が携わったプロジェクトとかを記述できます  

## section  
このセクションの情報の設定をします。  
  
### name  
このセクション名の設定をします。  
ナビゲーションバーに表示させる項目名になります。  

### id  
このセクションのidの設定をします。  

### enable  
このセクションの表示非表示を設定します。  
非表示にした場合は見えなくなります。  

true = 表示  
false = 非表示   

### weight  
ナビゲーションバーやページに表示させる順番を設定します  
数値が若いほうが優先されます。  
  

### showOnNavbar
ナビゲーションバーに表示させるか否かを設定します  

true = 表示  
false = 非表示   

### template
利用するテンプレートのHTMLファイルを指定します。  
カスタマイズしたときにこれで読み込ませることができると思われます。  

### hideTitle
ここをtrueにするとタイトル部分を隠すことができます。
  
## buttons
このセクションはフィルター機能を利用できるのですが、ここではそこで用意したいボタンを定義できます。  

### name
ボタン名

### filter
抽出したい属性

## projects
紹介したい自分が携わったプロジェクト等を好きなだけ記載していきます。  

### name
プロジェクト名やタイトルを記載します。  

### logo
なにかロゴとかを付けたいのであればここに画像を設定できます。
  
掲載したい場合は、  
assets内にimages/section/projectsディレクトリを作成しその中にロゴを配置します。
そしてここでは`"/images/sections/projects/XXXXXXX.png"`の様にimages以下から指定してあげます。  
   
### role
自分の役割なんかを記載していきます。  

### timeline
何時から何時までの期間携わったのかを記載できます。

### repo
gitのリポジトリを公開したい・できる場合はここにリンクを乗せましょう。

### url
サービスのURLがあり公開できる場合はここにリンクを張りましょう。

### summary
プロジェクトの概要をここに記載できます。

### tags
上記のフィルター機能に引っかかるようにカードにタグを与えられます。  
定義したfilterの値を同じ値を配列で定義してあげればOKです。  

こんな感じです。  
```console
tags: ["PowerShell", "Windows10", "自動化","bat","VBS"]
```  
