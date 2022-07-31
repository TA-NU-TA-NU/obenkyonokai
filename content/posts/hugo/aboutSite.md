---
title: "hugoで自サイト構築-Site.yaml編"
date: 2022-07-31T14:19:25+09:00
description: hugoで自サイト構築-Site.yaml編
menu:
  sidebar:
    name: hugoで自サイト構築-Site.yaml編
    identifier: hugo-aboutSite
    parent: hugo
    weight: 202
tags: ["hugo", "サイト構築"]
categories: ["hugo"]
---

## Site.yamlの設定について  
具体的にどんな位置付けねのかは表現しにくいのですが、サイトの諸設定等を行うファイルという感じですかね。  
  
## description
サイトディスクリプションの記述に相当する設定です。  
HTML上だと以下の記述に該当しますのでSEOや検索エンジンからの見え方を気にする場合は書きましょう。  
```htm
<meta name=description content="Portfolio and personal blog of Tack.">
```  
 

## customMenus 
カスタムメニューを個別に設定したい場合はここに記述します。  
  
### name
カスタムメニューに表示される文字列の設定  
  
### url  
参照するURLを記述します。  

### hideFromNavbar  
ナビゲーションバーに表示するか否かを設定できます。  

true=非表示  

false=表示  

### showOnFooter  
フッターに表示するか否かを設定できます。  
  
true=表示  

false=非表示  

## disclaimer  
免責事項の記述をできます。  
長くなってしまうなら専用ページ作ってリンクで飛ばしてしまう方がいいかもですね。  
  
