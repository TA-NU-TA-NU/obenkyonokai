---
title: "抽象クラスをつくる"
date: 2022-08-05T17:17:00+09:00
description: 抽象クラスをつくる
hero: images/posts/PowerShell/powershell.png
menu:
  sidebar:
    name: 抽象クラスをつくる
    identifier: PowerShell-AbstructClass
    parent: PowerShell
    weight: 104
mermaid: true
tags: ["PowerShell"]
categories: ["PowerShell"]
---

## 動機

折角クラスが使えるので、どこまでデザインパターンを充足できるのかという試み。  


## PowerShellによる抽象クラスの作成
最近までこれは不可能だと勝手に思っていたのですが、近しいことはできそうなのでここで試して見ます。  

参考として、  
結城浩さん著の『増補改訂版 Java言語で学ぶデザインパターン入門』より  
Template Methodパターンの例をPowerShellで実装してみましょう。  

## Template Methodパターン
最終的にはこんな感じになります。  
IncompleteDisplayクラスは比較のために不完全な実装によってちゃんと実体化できないクラスをあえて記述します  

{{< mermaid >}}
classDiagram
  AbstractDisplay <|-- CharDisplay : Inheritance
  AbstractDisplay <|-- StringDisplay : Inheritance
  AbstractDisplay <|-- IncompleteDisplay : ×
{{< /mermaid >}}

期待する動きとしては、  
CharDisplayでは文字をうけとったら<<>>で囲って5回文字を出力させます。（例では'H'）  

```powershell
<<HHHHHH>>  
```

StringDisplayでは文字をうけとったら+-+と｜で周囲を囲って中に5行入力された文字を出力させます。（例では'Hello!'）  

```powershell
+------------+
|Hello World!|
|Hello World!|
|Hello World!|
|Hello World!|
|Hello World!|
+------------+
```

そしてIncompleteDisplayでは文字をうけとったら+-+と｜で周囲を囲って中に5行入力された文字を出力させようとしますが実装が足りないため異常を発生させます。  

----------

## 抽象クラスをつくる

{{< mermaid align="left">}}
classDiagram
class AbstractDisplay{
  open()
  print()
  close()
  display()
}

{{< /mermaid >}}

```powershell
class AbstractDisplay {

    AbstractDisplay() {
        $type = $this.GetType()
        if ($type -eq [AbstractDisplay]) {
            throw("$type は 継承して利用してください")
        }
    }
    #抽象メソッド1 -> サブクラスに実装を任せる抽象メソッド
    hidden [void] open() {
        throw("オーバーライドしてください。")
    }

    #抽象メソッド2 -> サブクラスに実装を任せる抽象メソッド
    hidden [void] print() {
        throw("オーバーライドしてください。")
    }

    #抽象メソッド3 -> サブクラスに実装を任せる抽象メソッド
    hidden [void] close() {
        throw("オーバーライドしてください。")
    }

    #ここで実装する
    [void] display() {
        $this.open()
        for ($i = 0; $i -lt 5; $i++) {
            $this.print()
        }
        $this.close()
    }
}
```  

先ず自分がこの実装パターンに触れて感動したのはコンストラクタの部分ですね！  
コンストラクタを通る際に自身の型を確認して抽象クラスとして取り扱っている型ならthrowするという考え方は本当に驚きました  

同じく抽象メソッドとして扱う場合も同様に使われたらthrowします。  

実体化したときに使う側に見せる必要がないものはhiddenにしてます。

さて、ここで誤ってAbstractDisplayをnewして使おうとしましょう…  
```powershell
."~~~~\Display.ps1"
$cls = [AbstractDisplay]::new()   
Exception: ~~~~\Display.ps1:6:13
Line |
   6 |              throw("$type は 継承して利用してください")
     |              ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
     | AbstractDisplay は 継承して利用してください

```

というようなExceptionが返ってくるため異常に気づけますね！  


## サブクラスを作って実装させる

{{< mermaid align="left">}}
classDiagram
class CharDisplay{
  char ch
  open()
  print()
  close()
}
class StringDisplay{
  String string
  int width
  open()
  print()
  close()
  printLine()
}
{{< /mermaid >}}

```powershell
#AbstructDisplayに対して実装をした具体クラス
class CharDisplay:AbstractDisplay {
    [char] $ch

    CharDisplay([char] $ch) {
        $this.ch = $ch
    }

    hidden [void] open() {
        Write-Host -NoNewline "<<"
    }

    hidden [void] print() {
        Write-Host -NoNewline $this.ch
    }

    hidden [void] close() {
        Write-Host ">>"
    }
}

#AbstructDisplayに対して実装をした具体クラス
class StringDisplay:AbstractDisplay {
    [string] $string
    [int] $width

    hidden StringDisplay([String] $string) {
        $this.string = $string
        $this.width = [System.Text.Encoding]::GetEncoding("shift_jis").GetByteCount($string)
    }

    hidden [void] open() {
        $this.printLine()
    }

    hidden [void] print() {
        $decolatedLine =  "|" + $this.string + "|"
        Write-Host $decolatedLine
    }

    hidden [void] close() {
        $this.printLine()
    }

    hidden [void] printLine() {
        Write-Host -NoNewline "+"

        for ($i = 0; $i -lt $this.width; $i++) {
            Write-Host -NoNewline "-"
        }

        Write-Host "+"
    }
}
```  

各々具体クラスを用意して実装をしていきます  

実行してみましょう。

```powershell
."~~~~\Display.ps1"
[AbstractDisplay]$foo = [CharDisplay]::new([char]'H')
$foo.display()
<<HHHHH>>
[AbstractDisplay]$bar = [StringDisplay]::new('Hello World!')
$bar.display()
+------------+
|Hello World!|
|Hello World!|
|Hello World!|
|Hello World!|
|Hello World!|
+------------+
[AbstractDisplay]$piyo = [StringDisplay]::new('こんにちは！')
$piyo.display()
+------------+
|こんにちは！|
|こんにちは！|
|こんにちは！|
|こんにちは！|
|こんにちは！|
+------------+

```
…といった感じに出力されます。  

ですので、こんな風にできちゃいますね！  

```powershell
[AbstractDisplay[]]$store = @(
    [CharDisplay]::new([char]'H'),
    [StringDisplay]::new('Hello World!'),
    [StringDisplay]::new('こんにちは！')
)
foreach ($item in $store) {
    $item.display()
}
<<HHHHH>>
+------------+
|Hello World!|
|Hello World!|
|Hello World!|
|Hello World!|
|Hello World!|
+------------+
+------------+
|こんにちは！|
|こんにちは！|
|こんにちは！|
|こんにちは！|
|こんにちは！|
+------------+
```  

## 実装が不十分な場合

{{< mermaid align="left">}}
classDiagram
class IncompleteDisplay{
  String string
  int width
  open()
  print()
  printLine()
}

{{< /mermaid >}}

```powershell
#AbstructDisplayに対して不完全な実装をした具体クラス -> 実行時throw
class IncompleteDisplay:AbstractDisplay {
    [string] $string
    [int] $width

    IncompleteDisplay([String] $string) {
        $this.string = $string
        $this.width = [System.Text.Encoding]::GetEncoding("shift_jis").GetByteCount($string)
    }

    hidden [void] open() {
        $this.printLine()
    }

    hidden [void] print() {
        $decolatedLine =  "|" + $this.string + "|"
        Write-Host $decolatedLine
    }

    hidden [void] printLine() {
        Write-Host -NoNewline "+"

        for ($i = 0; $i -lt $this.width; $i++) {
            Write-Host -NoNewline "-"
        }

        Write-Host "+"
    }
}
```  

このように実装しなければいけないメソッドを一部実装しなかったとします。 



```powershell
."~~~~\Display.ps1"
[AbstractDisplay]$bad = [IncompleteDisplay]::new('Hello!')
bad.display() #Errorになる
+------+
|Hello!|
|Hello!|
|Hello!|
|Hello!|
|Hello!|
Exception: ~~~~\Display.ps1:21:9
Line |
  21 |          throw("オーバーライドしてください。")
     |          ~~~~~~~~~~~~~~~~~~~~~~~
     | オーバーライドしてください。

```

close()を呼び出したときにExceptionが返ってくるためこちらでも異常に気づけますね！  


