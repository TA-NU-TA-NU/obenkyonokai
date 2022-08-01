---
title: "hugoで自サイト構築-GitAction編"
date: 2022-08-01T23:28:00+09:00
description: hugoで自サイト構築-GitAction編
menu:
  sidebar:
    name: hugoで自サイト構築-GitAction編
    identifier: git-action
    parent: git
    weight: 204
tags: ["hugo", "サイト構築","git"]
categories: ["hugo","git"]
---
  
## gitActionと連携してサーバーへの自動デプロイをする
サイトができたらレンタルサーバーへの自動デプロイを可能にし、  
自身のブランチにpushされたらデプロイを自動でしてくれるようにします。  
  
## gitActionとは何ぞや  
GithubのCI/CDツールです。  
定義されている通りに任意の処理が走り、いろいろなことを自動化してくれます。  

自分が定義、あるいは共有されているActionやコマンドの実行を組み合わせ行くことで記述していきます。  

## 前提知識の整理
取り扱う際の前提知識を整理しておきます。

### Workflow
任意のイベントをトリガーに実行される複数のJobからなる自動化されたプロセスです。  
`.github/workflows/`ディレクトリを作成し、そこに任意の名前のyamlを作成します。  
このyamlが一つのworkflowファイルになります。  

### Job
Workflowを構成するStepのあつまり。  

### Step
stepは自分が定義、あるいは共有されているActionの利用やコマンドの実行によって構成される処理の集合  

### Action
ワークフローの最小構成要素。
use:による共有されているActionの利用やrunによるコマンドの実行など。

## 書いたやつ  
実際こんな感じで書きました。  
  
```console
name: Deploy

on:
  push:
    branches: [ master ]

jobs:

  build_and_deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
      with:
        submodules: true # Fetch Hugo themes (true OR recursive)
        fetch-depth: 0 # Fetch all history for .GitInfo and .Lastmod

    - name: Setup Hugo
      uses: peaceiris/actions-hugo@v2
      with:
        hugo-version: '0.101.0' #hugoのバージョンを記述
        extended: true

    - name: Build
      run: hugo --minify

    - name: List output files
      run: ls public/

    - name: FTP-Deploy-Action
      uses: SamKirkland/FTP-Deploy-Action@4.0.0   # FTPを使ってサーバーにDeployするアクションを実行
      with:                                        
        server: ${{ secrets.FTP_SERVER }}     # FTPサーバーのURLを設定
        username: ${{ secrets.FTP_USERNAME }} # FTPのユーザー名を設定
        password: ${{ secrets.FTP_PASSWORD }} # FTPのパスワードを設定
        local-dir: public/                           # どのディレクトリのデータをアップロードするか
        server-dir: /obenkyonokai.com/      # ロリポップ！FTPサーバのどのディレクトリにアップロードするか

```
  
### name
アクション名の定義  

### on
このアクションの実行のトリガーを記載

#### push
push時がこのworkflowのトリガーになります。   

##### branches
今回はmasterブランチにpush時をトリガーとしたいのでさらにbranchesとしてブランチ名を記載しました。  

### jobs
ここからジョブの詳細を記載  

この下の階層にジョブ名を定義します。今回はbuild_and_deployに相当。  

#### runs-on
実行環境をここで指定します。  
今回はubuntu  

#### steps
step単位で処理を記述・定義します。  
name:で名前も付けられます。  

#### uses: actions/checkout@v2
チェックアウトのactionを利用していきます。  
行いたい処理に合わせてwith:を与えていきます。  

※v3が利用できるんですね…
参考:[https://github.com/actions/checkout](https://github.com/actions/checkout)  

##### submodules: true
hugoのテーマをsubmoduleとして参照しているのでこれも合わせてチェックアウトします  

##### fetch-depth: 0
この指定で全てのブランチをタグの履歴を参照させます。  

#### uses: peaceiris/actions-hugo@v2
HugoのSetupとビルドを行う処理をここで定義します。  
その際はhugoから提供されているActionを利用していきます。

参考：[peaceiris/actions-hugo@v2](peaceiris/actions-hugo@v2)  
  
##### hugo-version: '0.101.0'
with:内でバージョンを与えてローカルで稼働確認できている利用したいversionを指定しましょう。  

##### extended: true
extended version も利用したい場合は true としておきます  

#### run: hugo --minify
run: は  コマンドの実行を指します。  
`hugo --minify` は hugoサイトをビルドするコマンドです。 --minifyオプションは圧縮してビルドさせるためのもの。  

#### uses: SamKirkland/FTP-Deploy-Action@4.0.0
FTPを使ってサーバーにDeployするアクションだそうです。

参考：[https://github.com/SamKirkland/FTP-Deploy-Action](https://github.com/SamKirkland/FTP-Deploy-Action)  

当初は2.0.0を利用していましたが、どうもこっちの方が実効速度が速いそうです。  
直近のworkflowの実行時間が 9m 2s だったものが 3m 38s になってました。  
二回目は 8m 1s...汗

※ちゃんとしたはかり方ではないけど…  

#### ${{ secrets.XXXXX }} 部分の定義
接続情報は秘匿化したいのでsecretsを使って隠蔽します。

GitHubのリポジトリ上の...  
Settings -> Secrets -> New repository secret から

以下の様にキーの作成をする
- FTP_SERVER -> FTPサーバーのURLを設定
- FTP_USERNAME -> FTPのユーザー名を設定
- FTP_PASSWORD -> FTPのパスワードを設定

## あとはデプロイ！
出来上がったら実際にpushすればよきまる。