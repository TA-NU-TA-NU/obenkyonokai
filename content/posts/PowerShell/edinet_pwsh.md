---
title: "EDINETAPIをPowerShellで触れてみた"
date: 2022-08-19T17:17:00+09:00
description: "EDINETAPIをPowerShellで触れてみた"
hero: images/posts/PowerShell/powershell.png
menu:
  sidebar:
    name: "EDINETAPIをPowerShellで触れてみた"
    identifier: PowerShell-edinet
    parent: PowerShell
    weight: 105
tags: ["PowerShell"]
categories: ["PowerShell"]
---

## 動機
EDINETAPIなるものを知ったのでそれをPowerShellで叩いてみたいと思った。  

## EDINET API とは  
先ず、EDINETというのは、金融庁が有価証券報告書などの開示書類を閲覧するためのサイトです。  

この開示システムには、EDINET APIというAPIが用意されています。

以下、EDINET_API仕様書.pdfより抜粋  

> EDINET API は、利用者が EDINET の画面からではなく、プログラムを介して EDINET の
データベースから効率的にデータを取得できる API（アプリケーション・プログラミング･
インターフェース）です。EDINET API により、EDINET 利用者は効率的に開示情報を取得
することが可能となります。  

そこで、このシステムにふれやすくなるような仕組を何らかの形で用意してあげられればWEBをポチポチする必要がなくなってより便利になるわけですね。  

## 実行方法  
大まかなながれとしては、メタデータを取得するエンドポイントにアクセスしてほしい情報を探します。  

そして、ほしい情報の文書を取得するエンドポイントにアクセスして任意の形式でファイルを取得します。  

### 各エンドポイントへのアクセスの概要
先ず、メタデータの取得にはREST形式で`https://disclosure.edinet-fsa.go.jp/api/[バージョン]/documents.json`に対してGETメソッドを用いてリクエストします。  

ちなみに、今回はバージョンについてはv1を使用しました.

パラメーターは
- date (YYYY-MM-DD 形式。最長5年前まで参照可能。)
- type（任意。 defalt は 1。1:=メタデータのみ 2:=提出書類一覧及びメタデータ）
とあります。

実際に使いたい場合はこんな感じですね。
`https://disclosure.edinet-fsa.go.jp/api/v1/documents.json?date=2022-08-08&type=2`

なので、
```PowerShell
#URL
$url = "https://disclosure.edinet-fsa.go.jp/api/v1/documents.json"

#以下をparamとしてとる
$getUrl2 = $url + "?date=2022-08-08&type=2"

#GETでアクセスして結果を絞る
$res= Invoke-RestMethod  $getUrl2
$res.results | Select-Object -Property 'docID','docDescription','filerName' | Where-Object -Property 'docDescription' -Match '四半期' 

#こんな感じにとれる
docID    docDescription                                                   filerName
-----    --------------                                                   ---------
S100OW42 四半期報告書－第75期第1四半期(令和4年4月1日－令和4年6月30日)     上新電機株式会社
S100OVTZ 四半期報告書－第58期第3四半期(令和4年4月1日－令和4年6月30日)     富士製薬工業株式会社
S100OUXV 四半期報告書－第209期第1四半期(令和4年4月1日－令和4年6月30日)    株式会社四国銀行
S100OVEF 四半期報告書－第73期第1四半期(令和4年4月1日－令和4年6月30日)     ナカバヤシ株式会社
S100OV58 四半期報告書－第51期第1四半期(令和4年4月1日－令和4年6月30日)     株式会社ＤＴＳ
（以下省略）
```

今度は任意のドキュメント取得をしてみます。  
ここでめぼしい書類を発見したらそのdocIDでもって  
`https://disclosure.edinet-fsa.go.jp/api/[バージョン]/documents/[欲しいdocID]`  
にアクセスします。

ここでもバージョンについてはv1を使用しました.
リクエストパラメーターは`type`というもののみがあります。

それぞれ以下のような設定値です
- 1:=基本文書及び監査報告書
- 2:=pdfで取得
- 3:=代替書面・添付文書
- 4:=英文ファイル

今回は1を選択してzipとして取得してみます。

```powershell
$getDocUrl="https://disclosure.edinet-fsa.go.jp/api/v1/documents/" + $res[0].docID + "?type=1"
Invoke-RestMethod  $getDocUrl -OutFile test.zip
```

## PowerShellでやってみたこと  
これらを上手にclassやfunctionでくるんで扱いやすくしてみました。  
粗削りですが。  

[edinetAccesser](https://github.com/TA-NU-TA-NU/edinetAccesser)