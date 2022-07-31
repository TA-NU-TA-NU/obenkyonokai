---
title: "hugoで自サイト構築-記事作成編"
date: 2022-07-31T16:39:00+09:00
hero: images/posts/hugo/hero.png
description: hugoで自サイト構築-記事作成編
menu:
  sidebar:
    name: hugoで自サイト構築-記事作成編
    identifier: hugo-aboutPosts
    parent: hugo
    weight: 208
tags: ["hugo", "サイト構築"]
categories: ["hugo"]
---

## 記事投稿について

記事の投稿についてはcontent/postsディレクトリを拡充していくことで行います。  

記事はマークダウンファイルに記事についての設定と内容を記述することで作成します。  

又、記事一覧の階層についてはcontent/posts内にディレクトリを作成して、それに合わせて_index.mdファイルをおいて設定を記述することで行います。 
  
## postsの作成
content/postsディレクトリ直下に_index.mdファイルを置きます。  
  
_index.mdファイルには設定を以下のように記載します  
  

```markdown
---
title: Posts
---
```  
  
ここでの記載はサイドバーのツリー最上段の記事を選択したときのタイトル名にあたります  
特にこだわりがなければのままでよいでしょう。  
  
## サブディレクトリの作成
記事を階層分けしたい場合はposts配下に任意のディレクトリを作成しましょう。  
  
そしてその中に_index.mdファイルをおいて設定を記載します。  
  
サンプルは以下  
```markdown
---
title: Hugo
menu:
  sidebar:
    name: Hugo
    identifier: hugo
    weight: 300
---
```
  

### title
ここは先ほど同じように選択した際のタイトル名ですね  
  
### menu/sidebar
ここではサイドバーでの表示のされかたの設定ができます。  
  
#### name  
サイドバーでの表示名の設定ができます。  
  
#### identifier  
階層構造を構成するためにこの階層を特定する必要があるのでidentifierを与えておきます  
  
#### weight  
表示優先度を定義します。若いほうがより上部に表示されます。
  
## 記事の作成  
  
あとは記事を作りたい階層に記事名.mdを作成します。  
そしてそのマークダウンファイルにその記事についての設定と記事の内容を記述していきます。  
  
サンプルは以下の通り…  
```markdown
---
title: "hugoで自サイト構築-投稿カテゴリ作成編"
date: 2022-07-31T16:39:00+09:00
description: hugoで自サイト構築-投稿カテゴリ作成編
menu:
  sidebar:
    name: hugoで自サイト構築-投稿カテゴリ作成編
    identifier: hugo-aboutCategory
    parent: hugo
    weight: 208
tags: ["hugo", "サイト構築"]
categories: ["hugo"]
---

```
  
### title
ページタイトル

### date  
作成日

### description
HTML上ではいかに相当するタグの内容の設定です。
```htm
<meta name="description" content="hugoで自サイト構築-投稿カテゴリ作成編">
```
  
検索エンジンからの見え方とか気にするならしっかりかくとよいと思います。  

### menu/sidebar
ここではサイドバーでの表示のされかたの設定ができます。  

#### name
サイドバーでの表示名の設定ができます。  

#### identifier
この記事を特定できるようにする必要があるのでidentifierを与えておきます  

#### parent
自身の親の階層のidentifierを指定する

#### weight
表示優先度を定義します。若いほうがより上部に表示されます。

### tags
タグを付与することができます。  
付与されたタグはタイトル直下に記載されます。  
又、`[URL]/tags/`で左袖にタグ一覧を出せる他`[URL]/tags/[tag名]`でタグごとに一覧をメイン画面に出力させることもできます。  

### categories
記事を任意でカテゴライズすることも可能です。  
その際は`categories: ["カテゴリ名"]`の様にします。

このカテゴリごとの一覧を表示したい場合は
`[URL]/categories/`で左袖にカテゴリ一覧を出せる他`[URL]/categories/[カテゴリ名]`でカテゴリごとの一覧をメイン画面に出力させることもできます。  

## 本文
以上で設定は完了なのでmd形式で本文を記述していくだけです