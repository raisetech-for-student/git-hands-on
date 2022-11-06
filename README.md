# 概要
Gitを初めて扱うひとのためのガイドプロジェクトです。

# ハンズオン

## お願い
- もし手順にあやまりがあればぜひ教えて下さい!
- 各コマンド実施時に表示されるメッセージはよく読みましょう!
  - 問題が起きていることに気づかずどんどんコマンド実行して気づいたらめちゃくちゃに・・・というのはあるあるです。
- エラーで困った際にはSlackなどでスクショや画面録画などをつかいつつ説明いただけると解決までの時間が早くなります!

## 準備

### Windowsの方
[Git for Windows](https://gitforwindows.org/) またはWSL2を準備してください。  
ターミナルを開いてください。  
<img src="https://user-images.githubusercontent.com/62045457/167234532-4e21a9c6-8ddd-4b74-bf6a-43bf7e0c22ca.png" width="300">

### Macの方
ターミナルを開いてください。  
<img width="300" alt="スクリーンショット 2022-05-07 11 37 40" src="https://user-images.githubusercontent.com/62045457/167234641-75dc9a20-a9d6-478b-8d2a-1502da4f216f.png">

### 共通
`$ git --version`  
を実行してgitのバージョン情報が表示されたら、スクショをとってSlackにて担当講師にてお知らせください。  
#課題提出チャンネルにて投稿お願いします。  

<img width="300" alt="スクリーンショット 2022-05-07 11 41 22" src="https://user-images.githubusercontent.com/62045457/167234787-2b5d8374-f666-4657-9e19-2ba34932780d.png">

## GitHubにてレポジトリを作成

まずはGitHubのアカウントを作成してください。  
次にレポジトリの作成をしてください。  

レポジトリ名: github-handson  
それ以外は何も入力しないでOKです。  
<img width="400" alt="スクリーンショット 2022-05-07 11 44 13" src="https://user-images.githubusercontent.com/62045457/167234889-33b60bf2-2f28-4341-9d5a-1d1518930b47.png">

レポジトリを作成すると下記画面に遷移します。  
<img width="400" alt="スクリーンショット 2022-05-07 11 44 54" src="https://user-images.githubusercontent.com/62045457/167234921-98251612-b7ba-45e3-95f4-f1252196987b.png">

> …or create a new repository on the command line

に今回使うコマンドがすでに記載されています。  
`git remote add origin ...`というコマンドをコピーしてメモ帳かなにかに残しておきましょう。  
ここまでできたら作成したレポジトリのリンクを前の手順で送ったSlackのメッセージのスレッドにてお知らせください。  

## ファイルを追加してpushする

ローカルPCからファイルをGitHubにpushします（アップロードに近いイメージ）。  

### プロジェクトの配置場所を作成

ターミナルを開きます。  

まず、プロジェクトを配置するディレクトリ（フォルダー）を作成します。  
ここが個人の環境によって変わる部分です。  
場所は任意ですが、例示しておきます。  

Windows  
`$ cd c:/`  
`$ mkdir projects`  
`$ cd projects`  
`$ pwd`  
c/projectsとなっていればOKです。  

Mac  
`$ mkdir projects`  
`$ cd projects`  
`$ pwd`  
/Users/PCのユーザー名/projectsとなっていればOKです。  

自分がどこにプロジェクトを配置したか忘れないようにメモしておきましょう。  
また、ソースコードをどこに置くかはOSや個人の好みによります。  
時間があるときでいいので`Windows ソースコード　置き場所`などで調べてみてください。  

### プロジェクトの作成

Gitで管理するプロジェクトを作成します。  

`$ pwd`  
projectsディレクトリ配下であることを確認する。  

`$ mkdir github-handson`  
`$ cd github-handson`  
`$ pwd`  
github-handsonディレクトリに移動できていることを確認する。  

ファイルを作成します。  
`$ echo "# github-handson" >> README.md`  
`$ ls`  
README.mdが表示されること。  
`$ cat README.md`  
`# github-handson`と表示されることを確認する。  

`$ git init`  
`Initialized empty Git repository`というようなメッセージが表示されることを確認する。  
黄色で注意文言が表示されると思うので読んでおきましょう。  
ブランチ名をmasterからmainに変更してください。  
`$ git branch -M main`  
`$ git status`
> On branch main

と表示されていればOKです。  
`$ ls -a`  
`.git`というディレクトリが作成されていることを確認する。  

`$ git status`  
表示内容を読む。  
<img width="500" alt="スクリーンショット 2022-05-07 12 21 20" src="https://user-images.githubusercontent.com/62045457/167236041-a3957b73-406f-4c78-9714-5ab108f032c3.png">

変更内容をインデックスに追加します。  
`$ git add .`  
`$ git status`  
表示内容を読む。  
> Changes to be committed

以下はこれからコミットする変更の一覧を表しています。  
<img width="500" alt="スクリーンショット 2022-05-07 12 23 14" src="https://user-images.githubusercontent.com/62045457/167236121-c2030587-7f2e-476f-bf7f-83bb79a38719.png">

変更内容をコミットします。  
`$ git commit -m "README.mdを追加"`  
<img width="500" alt="スクリーンショット 2022-05-07 12 27 04" src="https://user-images.githubusercontent.com/62045457/167236254-26480f06-8402-411d-9b6c-2dcf6c43b28e.png">

念の為コミットができているか確認をします。  
`$ git log`  
<img width="500" alt="スクリーンショット 2022-05-07 12 27 36" src="https://user-images.githubusercontent.com/62045457/167236292-3461cc14-1c8b-4e62-8e39-6d13e4a61fb8.png">  
ログは最初は読みづらいですが、今回は「README.mdを追加」という文言が表示されていることを確認してください。  

コミットができているか確認できたらGitHubにpushします。  
GitHubのどのレポジトリにpushするかを設定します。  
ただし、下記コマンドは「小山のレポジトリ」へpushすることになりますので自分のレポジトリ用にコピーして控えていたものを使ってください。  
`$ git remote add origin git@github.com:yoshi-koyama/github-handson.git`  

GitHubのmainブランチにpushします。  
`$ git push origin main -u`  
<img width="500" alt="スクリーンショット 2022-05-07 12 37 12" src="https://user-images.githubusercontent.com/62045457/167236636-a97dc855-6ccb-4f5c-aba4-6be72cb8abc0.png">  
※始めてGitHubにpushする人は認証が必要になります。 
認証方法はpush時に用いる通信方式がhttpsかsshかによって変わります。  

リモートブランチを下記コマンドで確認することができます。  
`$ git remote -v`  

sshの場合: `https://github.com/raisetech-for-student/git-hands-on.git`  

httpsの場合: `git@github.com:raisetech-for-student/git-hands-on.git`  

※このハンズオンの手順をそのまま実施していればssh方式になります。  

sshの場合、公開鍵と秘密鍵の作成とGitHubへの登録が必要になります。  
`ssh GitHub`で調べるとやり方がでてきます。  
公式ドキュメント: https://docs.github.com/en/authentication/connecting-to-github-with-ssh  

httpsの場合、個人アクセストークンを発行して認証に用いる必要があります。  
公式ドキュメント： [個人アクセストークンを使用する](https://docs.github.com/ja/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)  

また、こちらは任意課題ですが、`GitHub https`や`GiｔHub ssh`で調べてそれぞれの接続設定の違いを把握して対応しましょう。  

※mainブランチのブランチという考え方はぜひ自習してみてください。講義のなかでもまたご紹介します。  
※初回以降は`git push`でpushできます。  

push時にはerror、fatal、failed、rejectedなど何らかの問題が起きたようなメッセージが表示されていないかよく確認しましょう。  

pushできたらGitHubの自分のレポジトリにアクセスしてみましょう。  
README.mdがpushされているか確認してください。  
<img width="500" alt="スクリーンショット 2022-05-07 12 38 49" src="https://user-images.githubusercontent.com/62045457/167236673-5d641ab5-cc98-4c3a-911e-db4801ac1226.png">

ここまでできたらSlackにて完了報告とレポジトリのURLを再度お送りください!  
お疲れさまでした!  
