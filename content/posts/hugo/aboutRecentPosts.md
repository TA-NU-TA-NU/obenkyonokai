---
title: "hugoで自サイト構築-RecentPosts.yaml編"
date: 2022-07-31T16:39:00+09:00
description: hugoで自サイト構築-RecentPosts.yaml編
menu:
  sidebar:
    name: hugoで自サイト構築-RecentPosts.yaml編
    identifier: hugo-aboutRecentPosts
    parent: hugo
    weight: 207
tags: ["hugo", "サイト構築"]
categories: ["hugo"]
---
  
## RecentPosts.yamlの設定について  
このセクションでは自分が投稿した最近の記事を掲載する部分について記述できます  

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

