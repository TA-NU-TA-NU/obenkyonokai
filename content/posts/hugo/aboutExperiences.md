---
title: "hugoで自サイト構築-Experiences.yaml編"
date: 2022-07-31T15:56:00+09:00
description: hugoで自サイト構築-Experiences.yaml編
menu:
  sidebar:
    name: hugoで自サイト構築-Experiences.yaml編
    identifier: hugo-aboutExperiences
    parent: hugo
    weight: 205
tags: ["hugo", "サイト構築"]
categories: ["hugo"]
---
  
## Experiences.yamlの設定について  
このセクションは自分の来歴や経験とかを記述できます  

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
  
## experiences
自分の経験についての内容を設定できます。
記述順に表示されるようなので、経歴を昇順にするか降順にするかはここでの並び順に依存します。

### company
勤め先について記載します。

#### name
会社名を記載します。  

#### url
会社のurlを記載できます。  

#### location
会社の所在地を記載できます  

#### overview
会社や経験の概要を記載できます。

### positions
何をしていたかを記載できます。
様々な役職やポジションを経験している場合は複数記載できます。

#### designation
自分のポジション名や役割名、役職名などを記載できます。

#### start
いつからやっているのかを記載できます。  

#### end
いつまでやっているのかを記載できます。
ここを記載しない場合は"Present"となるので、現職の場合は記載しないようにします。

#### responsibilities
自分がそのポジションで行っていた仕事を簡単に記載しましょう。
