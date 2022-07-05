---
title: "hugoで自サイト構築導入編"
date: 2020-07-05T03:51:25+09:00
description: hugoで自サイト構築導入編
menu:
  sidebar:
    name: hugoで自サイト構築導入編
    identifier: hugo-aboutHugo
    parent: hugo
    weight: 10
tags: ["hugo", "サイト構築"]
categories: ["hugo"]
---

### Hugoとは
HugoとはGo言語で書かれた早くてモダンな静的サイトジェネレーターだそうで、簡単なwebサイトを手軽に構築できることから最近よく耳にするかと思います。  
<br>
Hugoはテンプレートに沿って設定や任意のファイルを加えてあげるだけで目的に合わせて基本的な機能を持ったWebサイトを構築できます。  
<br>
従来のWebサイト構築に伴う厄介な環境構築やデータベースの用意等は特段必要ないのもメリットです。  

[Hugo公式Top](https://gohugo.io/)  
 
このサイトもHugoにてテンプレートをお借りして構築しています。
このテンプレートにも目的に合わせて様々なものがありどれも素敵ですね。  
<br>

### Tohaとは  

で、今回は自分のアウトプットとポートフォリオの両方を叶えてくれるテンプレートを探しTohaというテンプレートにたどり着きました。  

これは、見事に自分のポートフォリオ＋ブログの両方の機能をもってドンピシャだったのでこれを基にサイトを構築していきました。  

[Tohaのサンプル](https://toha-guides.netlify.app/)  
<br>  

### 自分の環境について  
まず自分の環境についてですが、  
Windows10 HomeEditionにWSL2でUbuntu 20.04.3 LTSを展開しています。  
今回はそのUbuntu上で作業しています。  
<br>

#### install  
以下でインストールします。  

```console
sudo apt-get install hugo
```

インストールの確認については以下

```console
hugo version
```

v0.68.0以上であればTohaは適用可能だそうです  
<br>  

#### Hugoサイトのスケルトンの作成
サイトを作成したいディレクトリで以下のコマンドを実行します  
```console
hugo new site ./ -f=yaml --force
```

このコマンドを実行することでカレントディレクトリに対してhugoサイトのスケルトンを生成します。  
またこの時、`-f=yaml` とすることで自動生成されるconfigファイルをyaml形式に指定できます。  
※デフォはtoml
  
そして、`--force`とすることで対象ディレクトリが存在しなくても生成させることができます  
<br>  

#### gitのイニシャライズ  

```console
git init
```
<br>  


#### Tohaテーマの導入  

以下のコマンドで自分のレポジトリーのthemes/tohaにサブモジュールとして導入します。  

```console
git submodule add https://github.com/hugo-toha/toha.git themes/toha
```  
  
tohaテンプレートの元のリポジトリの最新の更新を自分のサイトが利用する形をとるのでsubmoduleで参照を持つことで楽で安定した管理と編集をしているっぽいですね…  
（gitよわよわの民のためこの理解で良いか不安だが…）  
<br>  

      
#### お試し実行  
  
これだけで基本の部分は導入で来ているのでローカルで動作を確認できるはずです。  
  
以下でローカルにサイトを立ち上げられます  

```console
hugo server -t toha -w
```  
  
立ち上げたらhttp://localhost:1313にアクセスできるかと思います。  
アクセスするとおそらくデフォルト状態なのですがもうサイトの体をなしているので驚きますね！  
  
ひとしきり確認し終えたらCtrl＋Cしておきましょう。  
  
### サイトの設定
この後は、Tohaテーマにそって設定等をしていきます。  
一先ず長くなったのでここまで…  
