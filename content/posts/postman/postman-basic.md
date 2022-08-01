---
title: "postmanでbasic認証通したい"
date: 2022-08-02T06:13:00+09:00
description: postmanでbasic認証通したい
menu:
  sidebar:
    name: postmanでbasic認証通したい
    identifier: postman-basic
    parent: postman
    weight: 101
tags: ["postman"]
categories: ["postman"]
---

## postmanでbasic認証通したい

postmanでbasic認証通したい時にどうしたかの記録

- [postmanでbasic認証通したい](#postmanでbasic認証通したい)
  - [1.1. 結論](#11-結論)
  - [1.2. 根拠](#12-根拠)
  - [1.3. 課題](#13-課題)

### 1.1. 結論

1. Authorization選択
2. Typeプルダウンから認証方式を選択（今回はBasic Auth 選んだ）
3. Username と Password 入力する

で送れる。

### 1.2. 根拠

 CUI上でcurlコマンドうって
 `curl ... -u〈User名〉:〈パスワード〉`
とやってるのと同じ結果がえられたよ

### 1.3. 課題

プルダウンには他の認証方式もサポートしているので
状況に合わせてそちらを選択しても同じ感じなのかなとおもう。

別の認証の時に試してみる