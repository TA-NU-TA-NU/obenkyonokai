---
title: "markdownlintについて"
date: 2022-08-02T05:58:00+09:00
description: markdownlintについて
menu:
  sidebar:
    name: markdownlintについて
    identifier: vscode-markdownlint
    parent: vscode
    weight: 100
tags: ["vscode", "markdownlint"]
categories: ["vscode"]
---

## 1. markdownklintについて

VSCodeから推奨されていたmarkdownklintを使ってみたところ  
非常に便利だったためまとめておく  

- [1. markdownklintについて](#1-markdownklintについて)
  - [1.1. 結論](#11-結論)
  - [1.2. 根拠](#12-根拠)
  - [1.3. 使いかた](#13-使いかた)
    - [1.3.1. 導入](#131-導入)
    - [1.3.2. 修正させてみる](#132-修正させてみる)
  - [1.4. 課題](#14-課題)

### 1.1. 結論

Lint機能は偉大  

### 1.2. 根拠  
  
Markdownを通常のtxtファイルの様にサクサク書きたいところではあるけど、  
改行やらスペースやら細々したところがうまくいっていない場合が多い。  

後でプレビューして見ると、
繋がっててほしくないところが繋がってたり  

改行がうまくいってなかったり  

色々と粗が目立ってしまうし、何よりそれの修正が大変。  

そこでmarkdownklintを使ってみると  
怪しい部分を明示してくれるし、  
ありがちな修正なら一発で補正してくれるのでストレスが減る。  

### 1.3. 使いかた

#### 1.3.1. 導入

1. markdownklintをプラグインの検索窓から検索  

2. インストール  

3. markdownファイルに不備があれば「問題」タブにいろいろ書かれる。又、編集中のファイルにも黄色い波線が入る  

※ここら辺は他の似たようなプラグインとおんなじ。

#### 1.3.2. 修正させてみる

一通り書き終わってLintの指摘事項にそって自動修正してほしい場合。以下を実行

1. [Ctrl] + [Shift] + [P] でコマンドパレット開く

2. Fix all supported markdownlint violations in the document と入力

3. 実行

4. とても便利で我にっこり。

以上でクイックフィックスできそうな部分の修正をしてくれる  

### 1.4. 課題

もっといろいろ便利な機能を導入していってアウトプットにおけるQOLあげたい所存。
