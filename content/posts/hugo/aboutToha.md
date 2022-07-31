---
title: hugoで自サイト構築-config.yaml設定編
date: 2022-07-05T22:56:00+09:00
description: hugoで自サイト構築-config.yaml設定編
menu:
  sidebar:
    name: hugoで自サイト構築-config.yaml設定編
    identifier: hugo-aboutToha
    parent: hugo
    weight: 201
tags: ["toha", "サイト構築"]
categories: ["hugo"]
---
  
## ディレクトリの大まかな構成  

この記事を書いている時点でのディレクトリが以下のような構成になっています。  
  
{{< img src="/posts/img/directory_sample.png" title="directory" >}}

{{< vs 3 >}}

このテンプレートいじっていて重要なセクションについて、  
気づいたことやここら辺のディレクトリはこういうものかなみたいな事を簡単に示します。  
だいぶ荒いですけど…
<br>

### assets/images
ポートフォリオ向けのyamlやconfig.yaml等で設定する際に参照先となる画像ファイルの保存先だと思われます。  
  
各yamlではポートフォリオ画面やサイト、サイトオーナーなどについての記述や設定を記載できるのですが（詳細は後述）  
そこで必要となるファイルを必要なyamlのファイル名やディレクトリに合わせて保管しています。  
<br>

### content/notes  
blog機能実現している部分の一つですね。
当サイトのNoteでの投稿セクションに利用しました。  
今後ここにコンテンツを追加することでNoteが拡充されるかと…  
<br>  

### content/posts  
blog機能実現している部分の一つですね。
今ご覧になっている記事を構成するディレクトリです。  
<br>

### data
ポートフォリオを構成するディレクトリですね。  
設定項目ごとにyamlファイルを用意していきそこに任意の設定をしていくことで自分なりのポートフォリオサイトができます。  

又jpディレクトリ以外を作ることで他言語にも対応可能です。  

## config.yamlの設定  
以前の操作で生成されたconfig.yamlに設定を記述していきます。  
  
このファイルはこのサイトの基本的な設定を記述できる部分です。

### baseURL
サイトの公開用URLをここに記載します  

### languageCode  
hugoは他言語対応サイトを構築できます。  
そのための設定として言語や言語ごとのサイトの振る舞いを変更できる項目が設けられています。  
languageCode はRSSによってWebサイトの更新情報を配布するためlanguageエレメントに何を記載するかを規定します。  
日本語でのみの利用なら"ja"でよいかと思います。

### DefaultContentLanguage  
どの言語をデフォルトとして設定するかを規定できます。  
  
### title  
サイトタイトル  
  
### theme  
利用しているテーマの設定をします。今回はtohaを利用させて頂いていますのでこの"toha"と入力します。  

### languages
このセクションにはサイトが取り扱う言語について記載します。  

#### jp
今回は日本語なのでjpのみです。  
複数言語の場合にはこのセクションを増やしてあげると良いです。  

#### languageName
languageNameには表記したい文字列を記載するようです。

#### weight
weightには表示の優先度を数値で記載します。

### enableEmoji
絵文字の有効化無効化 :rofl:

#### enable  
有効化することで絵文字を記述できるようになります。:v:

### markup
TOCの対象についての設定ができます

#### tableOfContents
TOCに含める深さの設定

##### startLevel/endLevel
h2 ~ h6までを数値で範囲指定できます

##### ordered
番号をつけるか否かを設定できます
  
### params
ここの配下にはサイトのパラメーターについての記述を行います。

#### background
読み込ませたい背景画像のパスを設定します。
assets内にimagesディレクトリを作成しその中にsiteディレクトリを作成します。
背景画像はその中に配置すると読み込んでくれるみたいです。

#### logo
読み込ませたいロゴ画像のパスを設定します。

##### main
メインロゴを指定します。

##### inverted
ナビゲーションバーの初期位置の反転ロゴを指定します。

##### favicon
ファビコンを指定します

#### topNavbar
ナビゲーションバーに表示させる項目の最大数を設定します。
あふれた分（weightによる重み付けで序列が低いもの）は畳みこまれる。

#### darkMode
ダークモードについての設定

##### enable
ダークモードを設定するかどうかをtrue/falseで記述

##### provider
これは現在darkreaderのみサポートしているそうです

##### default
初期設定値を記載します。
system/light/darkから指定可能です。

#### features
tohaではポートフォリオサイトやblog,Notes,comment等の機能を利用できます。
ここでは、それらの機能の設定が可能です

##### portfolio
ポートフォリオ機能についての設定を記述しますできます

###### enable
ポートフォリオ機能の有効化無効化をtrue/falseで設定できます

##### blog
ブログ機能についての設定を記述しますできます

###### enable
ブログ機能の有効化無効化をtrue/falseで設定できます

###### shareButtons
各種シェアボタンの有効化無効化ができます

##### notes
ノート機能についての設定を記述しますできます

###### enable
ノート機能の有効化無効化をtrue/falseで設定できます

##### comment
コメント機能についての設定を記述しますできます

###### enable
コメント機能の有効化無効化をtrue/falseで設定できます

#### enableTOC
目次の利用の有効化無効化をtrue/falseで設定できます

#### enableTags
投稿ページにタグを表示するか否かの設定

#### showFlags
言語選択部分に国旗を表示焦るかどうかの設定 

#### footer
フッターの機能に関する設定ができます

##### enable 
フッターの表示非表示

##### template
デフォルトはfooter.html。  
多分独自カスタマイズののテンプレートを自身のレポジトリのlayouts/partialsにおいてあげるとそれを読み込んでくれるっぽい。  

##### navigation  
フッターのナビゲーション部分の設定

###### enable
フッターのナビゲーション部分の有効化無効化  
  
###### customMenus
フッターのナビゲーション部分にカスタムメニューを入れるか入れないか  
  
##### contactMe  
連絡先の表示についての設定

###### enable  
連絡先の表示非表示  

##### credentials
資格情報についての設定

###### enable  
資格情報の表示非表示  

##### newsletter
メール配信サービスの設定

###### enable  
メール配信サービス部分の表示非表示  

###### provider  
プロバイダーの設定  
※今はMailchimpのみをサポートしている様です。

###### mailchimpURL
mailchimpURLを設定することで連携できるっぽい。  
（このサービスについて詳しくないので不明ですが…）
  
##### disclaimer
免責事項の記載についての設定  
※記載内容はsite.yaml内で設定したdisclaimer内の記述に準じます

###### enable  
免責事項の記載の表示非表示  
