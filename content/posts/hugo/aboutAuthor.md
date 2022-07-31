---
title: "hugoで自サイト構築-Author.yaml編"
date: 2022-07-31T14:39:00+09:00
description: hugoで自サイト構築-Author.yaml編
menu:
  sidebar:
    name: hugoで自サイト構築-Author.yaml編
    identifier: hugo-aboutAuthor
    parent: hugo
    weight: 203
tags: ["hugo", "サイト構築"]
categories: ["hugo"]
---
  
## Author.yamlの設定について  
自分の基本情報について記載する箇所になります。  
  
## nickname
自分のニックネームの設定ですね。  
  
## image  
自分のイメージ画像を設定します。  
画像の格納場所は`assets/images/author`になるのでない場合はディレクトリを作ります。  
項目に記述するときは`images/author/XXXXXX.png`でよいみたいです。  
  
## greeting
デフォだと”Hi, I am” + (設定したニックネーム)のようになります。  
特に気にしなければ”Hi, I am”でいいかなって思ってます。  
  
## contactInfo
連絡先の記述ですね。  
config.yamlのcontactMeを有効にしていればここに記載した連絡先が表示されます。  
  
### email  
メアド  

### phone  
電話番号  
  
## summary  
トップ画面の”Hi, I am”の下部に表示される文字列を記述します。  
自分の場合は以下のように設定しているので、
```console
summary:
  - エンジニアをしてます!
  - このサイトは自分のポートフォリオ兼技術ブログとなっております！
  - 興味の向くままにおべんきょしてます！
  - マイペース更新ですが宜しくお願い致します！
```
これらが表示されているかと思います。  
  
自己紹介や、何をしているか、どんなサイトなのか等を端的に記載するとよいですね  
  
