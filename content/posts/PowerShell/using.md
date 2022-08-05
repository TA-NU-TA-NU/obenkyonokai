---
title: "usingについて"
date: 2022-08-05T12:42:00+09:00
description: usingについて
hero: images/posts/PowerShell/powershell.png
menu:
  sidebar:
    name: usingについて
    identifier: PowerShell-Using
    parent: PowerShell
    weight: 103
tags: ["PowerShell"]
categories: ["PowerShell"]
---

## 動機

PowerShellは自身が備えているコマンドレットだけでなく、.NET等を盛り込んでかなり柔軟にコーディングできます。  

しかしながら、  
呼び出すたびに凄い長い名前空間を記述する必要があるのが面倒なのでこれをどうにかしたい…  
  

## Usingを使って名前空間を省略する
そんな時はUsingを使うといいみたい。  

実際に使って比較してみます。  

----------

**Before**  

```powershell

$foo=[System.Text.StringBuilder]::new()

$foo.Append("Hello")
$foo.ToString() #Hello

$foo.Append(" World!")
$foo.ToString() #Hello World!

```  

この場合、  
StringBuilderを呼び込む時が面倒です…  
この程度のコード量なら大した苦痛はないですが、量が増えてきたらいちいちめんどうかと…  


----------

**After**  

```powershell
using namespace System.Text
$foo=[StringBuilder]::new()

$foo.Append("Hello")
$foo.ToString() #Hello

$foo.Append(" World!")
$foo.ToString() #Hello World!

```  

なので、このように`using namespace System.Text`としてあらかじめ宣言しておくと何度も書く必要がないので便利です。  
