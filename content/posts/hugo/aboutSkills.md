---
title: "hugoで自サイト構築-Skills.yaml編"
date: 2022-07-31T15:43:00+09:00
description: hugoで自サイト構築-Skills.yaml編
menu:
  sidebar:
    name: hugoで自サイト構築-Skills.yaml編
    identifier: hugo-aboutSkills
    parent: hugo
    weight: 205
tags: ["hugo", "サイト構築"]
categories: ["hugo"]
---
  
## Skills.yamlの設定について  
このセクションは自分のスキルとかを記述できます  

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
  
## skills
自分のスキルについて簡単に記述したカードの内容を設定できます。

### name
スキル名を記載します。

### logo
ロゴを合わせて表示できます。なければ省略されます。
  
掲載したい場合は、  
assets内にimages/section/skillsディレクトリを作成しその中にロゴを配置します。
そしてここでは`"/images/sections/skills/powershell.png"`の様にimages以下から指定してあげます。  
  

### summary
サマリーを記述できます。
