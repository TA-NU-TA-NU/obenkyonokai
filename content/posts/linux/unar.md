---
title: "unarについて"
date: 2022-08-02T21:08:00+09:00
description: unarについて
menu:
  sidebar:
    name: unarについて
    identifier: linux-unar
    parent: linux
    weight: 102
tags: ["linux"]
categories: ["linux"]
---

## 1. unarについて

windowsでzip化されているものを安全にlinux上で解凍したい  

- [1. unarについて](#1-unarについて)
  - [1.1. 結論](#11-結論)
  - [1.2. unar とは](#12-unar-とは)
    - [1.2.1. メリット](#121-メリット)
    - [1.2.2. 導入](#122-導入)
    - [1.2.3. 使い方](#123-使い方)

## 1.1. 結論  

unar コマンドがよろしいかとおもった  

## 1.2. unar とは  

linux上で使える圧縮ファイルの解凍のためのコマンドの一つ  

### 1.2.1. メリット

自分なりのメリットとしてはzip解凍時の文字化けを防げるいう点が大きいかなと  
自分はWSL2上のLinux Distribution で Ubuntuを動かしている関係上  
ホスト（Windows OS）側からLinuxにファイルを送りたいときがある。  
  
そんな時にWindowsから送ったzipが文字コードの関係で文字化けするときがある  

unarコマンドは文字コードの判別機能が備わっているらしく  
他のコマンドでは回避のためにオプションをつけたりするが、
unarの場合は特段いらないのでラク。  

### 1.2.2. 導入

以下コマンドで導入しておく  
`sudo apt install unar`

### 1.2.3. 使い方

単純な解凍ならこれだけ。  

`unar [解凍したいファイル]`