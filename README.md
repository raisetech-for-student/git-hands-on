# 概要
Gitを初めて扱うひとのためのガイドプロジェクトです。

# ハンズオン

## お願い
- もし手順にあやまりがあればぜひ教えて下さい!
- 各コマンド実施時に表示されるメッセージはよく読みましょう!
  - 問題が起きていることに気づかずどんどんコマンド実行して気づいたらめちゃくちゃに・・・というのはあるあるです。
- エラーで困った際にはチャットなどでスクショや画面録画などをつかいつつ説明いただけると解決までの時間が早くなります!
- わからない言葉やコマンドはぜひ調べてください!
  - このハンズオンでは専門用語を把握しなくてもGitの基本的な操作はできるようになることを目的としています。
  - しかし、Gitを使う上で専門用語は避けて通れません。ハンズオン完了後や別課題の合間でよいので調べてみてください。  

## 準備

### Windowsの方
[Git for Windows](https://gitforwindows.org/) またはWSL2を準備してください。  
ターミナルを開いてください。  
<img src="https://user-images.githubusercontent.com/62045457/167234532-4e21a9c6-8ddd-4b74-bf6a-43bf7e0c22ca.png" width="300">

WSL2を使う場合はWindowsの公式インストール手順を参考にしてください。  
WindowsでのWeb開発にWSL2は必要になりますが、インストールでつまってしまう場合、今はGitのみの利用なのでGit for Windowsをインストールしましょう。

### Macの方
ターミナルを開いてください。  
<img width="300" alt="スクリーンショット 2022-05-07 11 37 40" src="https://user-images.githubusercontent.com/62045457/167234641-75dc9a20-a9d6-478b-8d2a-1502da4f216f.png">

### 共通
```shell
$ git --version
```  
を実行してgitのバージョン情報が表示されたらOKです。  

<img width="300" alt="スクリーンショット 2022-05-07 11 41 22" src="https://user-images.githubusercontent.com/62045457/167234787-2b5d8374-f666-4657-9e19-2ba34932780d.png">

## Gitの初期設定

GitHubに登録したユーザー名とメールアドレスの設定を下記のように実行してください。   

```shell
$ git config --global user.name "GitHubのユーザー名"
$ git config --global user.email GitHubに登録しているメールアドレス
```

## GitHub 個人アクセストークンの作成
- [公式サイト](https://docs.github.com/ja/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)や他のサイトを見ながら、GitHub 個人アクセストークンを作成してください。
- 二種類ありますが`Fine-grained personal access tokens`が推奨です。
- 有効期限は無期限で構いませんが、無くしたり盗まれたりしないようにしてください。
- 書き込み権限は明示的に与える必要があります。忘れるとこの後 push で躓くので注意しましょう。以下のいずれかで可能です。

| 方式                                  | 操作                                                                                                                                    |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `Fine-grained personal access tokens` | `Repository access`・・・`All repositories`または作成済の操作したいリポジトリを選ぶ<br>`Permissions`・・・`contents` : `Read and write` |
| `classic`                             | リポジトリを条件に含められないので `repo`にチェック。    |

## GitHubにてリポジトリを作成

まずはGitHubのアカウントを作成してください。  
公式サイトやブログ記事、Qiitaなどを参考にしてください。  
GitHub公式サイト: https://docs.github.com/ja/get-started/signing-up-for-github/signing-up-for-a-new-github-account

次にリポジトリの作成をしてください。

リポジトリ名: github-handson  
それ以外は何も入力しないでOKです。  
<img width="400" alt="スクリーンショット 2022-05-07 11 44 13" src="https://user-images.githubusercontent.com/62045457/167234889-33b60bf2-2f28-4341-9d5a-1d1518930b47.png">

リポジトリを作成すると下記画面に遷移します。  
<img width="400" alt="スクリーンショット 2022-05-07 11 44 54" src="https://user-images.githubusercontent.com/62045457/167234921-98251612-b7ba-45e3-95f4-f1252196987b.png">

> …or create a new repository on the command line

に今回使うコマンドがすでに記載されています。  
`git remote add origin ...`というコマンドをコピーしてメモ帳かなにかに残しておきましょう。
なお、そのときにキャプチャの赤丸部分がHTTPSを選択していることに注意してください。  

### プロジェクトの配置場所を作成

ターミナルを開きます。  

まず、プロジェクトを配置するディレクトリ（フォルダー）を作成します。  
ここは個人の環境によって変わる部分です。  
場所は任意ですが、例示しておきます。

ディレクトリの作成はコマンドを使います。
コマンドの先頭にある`$`はコマンドを実行することを意味します。  
`$`は入力しないでください。

Windows  
```shell
$ cd c:/  
$ mkdir projects  
$ cd projects  
$ pwd
```  
c/projectsとなっていればOKです。  

Mac  
```shell
$ mkdir projects  
$ cd projects  
$ pwd
```

/Users/PCのユーザー名/projectsとなっていればOKです。  

自分がどこにプロジェクトを配置したか忘れないようにメモしておきましょう。  
また、ソースコードをどこに置くかはOSや個人の好みによります。  
時間があるときでいいので`Windows ソースコード 置き場所`などで調べてみてください。  

### プロジェクトの作成

Gitで管理するプロジェクトを作成します。  

```shell
$ pwd
```  
projectsディレクトリ配下であることを確認する。  

github-handsonディレクトリを作成して移動します。
```shell
$ mkdir github-handson  
$ cd github-handson  
$ pwd
```

github-handsonディレクトリに移動できていることを確認する。

### ファイルの作成
ファイルを作成します。  
```shell
$ echo "# github-handson" >> README.md  
$ ls
```

README.mdが表示されること。  
```shell
$ cat README.md
```  
`# github-handson`と表示されることを確認する。  

### リポジトリの初期化

```shell
$ git init
```  
`Initialized empty Git repository`というようなメッセージが表示されることを確認する。  
ブランチ名をmasterからmainに変更してください。  
```shell
$ git branch -M main  
$ git status
```
> On branch main

と表示されていればOKです。  
```shell
$ ls -a
```  
`.git`というディレクトリが作成されていることを確認しましょう。  

### ステージング（add）
まずは
```shell
$ git status
```  
を実行して表示内容を読む。  
<img width="500" alt="スクリーンショット 2022-05-07 12 21 20" src="https://user-images.githubusercontent.com/62045457/167236041-a3957b73-406f-4c78-9714-5ab108f032c3.png">

変更内容をステージング（add）します。    
```shell
$ git add .  
$ git status
```  
表示内容を読む。  
Changes to be committed以下はこれからコミットする変更の一覧を表しています。  
<img width="500" alt="スクリーンショット 2022-05-07 12 23 14" src="https://user-images.githubusercontent.com/62045457/167236121-c2030587-7f2e-476f-bf7f-83bb79a38719.png">

### コミット（commit）
変更内容をコミットします。  
```shell
$ git commit -m "README.mdを追加"
```  
<img width="500" alt="スクリーンショット 2022-05-07 12 27 04" src="https://user-images.githubusercontent.com/62045457/167236254-26480f06-8402-411d-9b6c-2dcf6c43b28e.png">

念の為コミットができているか確認をします。  
```shell
$ git log
```  
<img width="500" alt="スクリーンショット 2022-05-07 12 27 36" src="https://user-images.githubusercontent.com/62045457/167236292-3461cc14-1c8b-4e62-8e39-6d13e4a61fb8.png">

ログは最初は読みづらいですが、今回は「README.mdを追加」という文言が表示されていることを確認してください。  

コミットができているか確認できたらGitHubにpushします。  
GitHubのどのリポジトリにpushするかを設定します。  
ただし、下記コマンドは「小山のリポジトリ」へpushすることになりますので自分のリポジトリ用にコピーして控えていたものを使ってください。  
```shell
$ git remote add origin https://github.com/yoshi-koyama/github-handson.git
```  

### プッシュ（push）
GitHubのmainブランチにpushします。  
```shell
$ git push origin main -u
```  
<img width="500" alt="スクリーンショット 2022-05-07 12 37 12" src="https://user-images.githubusercontent.com/62045457/167236636-a97dc855-6ccb-4f5c-aba4-6be72cb8abc0.png">

GitHub のユーザー名とパスワードを聞かれますので入力してください。  
ユーザー名はアカウント開設したときの名称で、リポジトリ URL に含まれています。  
パスワードは、GitHub 個人アクセストークン（PAT）です。  
すでにお伝えしたとおりですが、PAT で書き込み権限が与えられていないとエラーになります。  
また、パスワードは入力しても表示されませんが、入力されています。  
これは盗み見に対するセキュリティ対策です。  

push時にはerror、fatal、failed、rejectedなど何らかの問題が起きたようなメッセージが表示されていないかよく確認しましょう。  

pushできたらGitHubの自分のリポジトリにアクセスしてみましょう。  
README.mdがpushされているか確認してください。  
<img width="500" alt="スクリーンショット 2022-05-07 12 38 49" src="https://user-images.githubusercontent.com/62045457/167236673-5d641ab5-cc98-4c3a-911e-db4801ac1226.png">

お疲れさまでした!  
