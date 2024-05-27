---
title: Git/GitHub研修(2)
directory: gh_2
theme: default
layout: quote
---

# Git/GitHub研修(第2回)

Klef Project ・ Klef Lab  
Powered by <span class="text-red-400">[Slidev](https://ja.sli.dev) </span>

---

# git clone

リモートのgitリポジトリをダウンロード(=<Highlight>クローン</Highlight>)する

チーム開発では誰かが作ったリポジトリをクローンして作業を始めることが多い

```bash
git clone https://github.com/klef-project/lecrure.git
```

↑のURLはこのリポジトリのURL
---

# Gitでファイルを管理する流れ

1. ファイルを作成or変更
2. `git add`で「<Highlight>ステージングエリア</Highlight>」に追加
3. `git commit`で変更をGitに記録(=<Highlight>コミット</Highlight>)
4. `git push`でリモートに送信(=<Highlight>プッシュ</Highlight>)

(チーム開発の場合)
1. `git fetch`でリモートの変更を確認(=<Highlight>フェッチ</Highlight>)
(変更がある場合)
2. `git pull`でローカルに反映(=<Highlight>プル</Highlight>)
以降上と同じ

---

# git add

ファイルをステージングエリアに追加

<Highlight>ステージングエリア</Highlight>(または<Highlight>インデックス</Highlight>)：次の「コミット」で変更を記録するファイルの一時置き場

```bash
git add -a # 変更されたファイルをすべてステージングエリアへ
git add file.txt # file.txtだけステージングエリアへ
git add ./src/sample.txt # ./src/sample.txtをステージングエリアへ
```

<br />

# git commit

ステージングエリア内のファイルの変更を記録(=<Highlight>コミット</Highlight>)

コミット時には<Highlight>コミットメッセージ</Highlight>が必要

```bash
git commit -m "My First Commit" # "My First Commit"というコミットメッセージをつけてコミット
```

---

# git push

コミットした内容をリモートに送信(=<Highlight>プッシュ</Highlight>)

コミットしただけではまだその記録はローカルにしかないので、リモートと同期

```bash
git push --set-upstream origin main # 1回目のプッシュのときはプッシュ先を指定
git push # 2回目以降はgit pushのみでOK
```

<br />

# git fetch

ローカルよりも新しいバージョンのリモートがないか確認

ローカルで作業している間にリモートが変更されていないか確認するコマンド

```bash
git fetch #特にオプションはない
```

---

# git pull

リモートの変更をローカルに適用(=<Highlight>プル</Highlight>)

`git fetch`の際にリモートが変更されていた場合に、ローカルをリモートに合わせて更新

```bash
git pull # オプションはなくはないがめったに使わない
```

<br />

# git status

迷ったときの便利コマンド

「今どのファイルがステージングエリアにあって、どのファイルが変更されて、~」というのを一覧表示してくれる

```bash
git status # 殆どの場合オプションは付けない
```

---

<img src="gh2/status.png" height="320" />

---

![Gitフロー](gh2/git_flow.drawio.png)

---

# 失敗したときの対応

1. ステージエリアにコミットしたくないファイルを入れてしまった場合
  →`git restore`を使用
2. コミットしたあとにそのコミットを取り消したい
  →`git revert`を使用
3. ステージエリアに入れていないが、保存したファイルを戻したい
  →`git stash`を使用
4. 新しいファイルをgitの管理下に置きたくなかったのになぜか入ってしまっていた
  →`git rm`を使用

---

# git restore

ステージエリアへの登録の取り消し

「コミットは細かくすべき」という大原則もあるので知っておこう

```bash
git restore file.txt # file.txtをステージング取り消し
git restore ./src/index.html # ./src/配下のindex.htmlのステージング取り消し
```

<br />

# git revert

コミットの打ち消し

厳密にはコミットの打ち消しコミットの作成

```bash
git revert HEAD # 最新のコミットの打ち消し
```

---

# git stash

gitに登録されている状態まで戻す

作業中にコミット前で実装していたものがいらなくなるのはよくあること

```bash
git stash -a # すべて取り消し
git stash file.txt # file.txtのみ取り消し
```

<br />

# git rm

gitにインデックス登録されているファイルの追跡取り消し

`/node_modules/`とか~~いらないのに~~なぜかインデックス登録される

```bash
git rm yarn.lock # yarn.lockをインデックスから削除
git rm -rf ./node_modules/ # ディレクトリ単位のときは-rオプション、node_modulesは地味に厄介だから強制削除の-f
```

---

# git log

gitのコミットのログが見れる

ここで見れる「SHA-1」はたまに参照することがある  
※SHA-1はこの文字列特有の名称ではなく、ハッシュ値の形式

```bash
git log # オプションはいろいろあるがひとまずなくてもOK
```

<br />

# clear

現在の表示内容を消去する(たいていどのシェルでも使える)

gitとは関係ないが何かと使える  
`git status`や`git log`でターミナルがごちゃついてきたときに有効

```bash
clear # オプションなどない
```

---

![git log](gh2/log.png)

---

# ブランチについて

branchの概念

<Highlight>ブランチ</Highlight>：現在の作業から<Highlight>枝分かれさせて</Highlight>現在の作業環境に影響を与えずに並行して別の作業を行える機能

<br />
<br />

## ブランチの利点

- <Highlight>大元のブランチに影響を与えず</Highlight>に異なる作業を<Highlight>複数人が同時に</Highlight>行える
- 別の人が同じところを変更した際に微妙に違うことが原因で発生する衝突(コンフリクト)が起こらない
- 実装する予定だったものが実装しないことになったときに対応がしやすい

## 用語

- ブランチを切る：ブランチを作成する

---

# git branch

ブランチの作成・削除・名称変更

ブランチに関する作業は基本的にこのコマンドで行う

```bash
git branch develop # developブランチを作成
git branch rm feature/csv # feature/csvブランチを削除
git branch rename csv feature/csv # csvブランチをfeature/csvブランチに変更
```

<br />

# git checkout

カレントブランチの変更(=<Highlight>チェックアウト</Highlight>)

カレントブランチ：今作業しているブランチ  
作業しているブランチを間違えていたとしても、コミットする前にチェックアウトすれば問題ない

```bash
git checkout develop # developにチェックアウト
```



---

# GitHub CLI

GitHubのCLIツール

GitHubで作業するときに、一回一回ブラウザで開くのも面倒なので、コマンドでできるのを紹介

## 今回取り扱う内容
- リポジトリの作成
- リポジトリのクローン
- Issueの表示
- Pull Requestの作成

## インストール

Winget経由が一番簡単

```ps
winget install --id GitHub.cli
```

---

## ログイン

GitHub CLIを使うには(当然)ログインが必要

```bash
gh auth login
```

What account do you want to log into? → github.com  
What is your preferred protocol for Git ~ → HTTPS
Authenticate Git with your GitHub credentials? → Y
How would you like to authenticate GitHub CLI? → Login with a web browser

を選択

エディターも変更しておくと何かと便利

```bash
gh config set editor "code --wait" # VSCode
```

---

## リポジトリ作成

```bash
gh repo create test --public # testという名称のパブリックリポジトリを作成
gh repo create test_private --private # test_privateというプライベートリポジトリを作成
```

<br />

## クローン

```bash
gh repo clone Klef-Project/lecture # owner/repository 形式で指定するだけ
```
↑例によってこの資料のリポジトリ

<br />
<br />

## Issueの表示

```bash
gh issue list
```

<br />

## Pull Requestの作成

```bash
gh pr create --base main --head develop --title "add header" # develop→mainに"add header"というタイトルのPRを作成
gh pr create --base develop # 現在のブランチ→developにPR作成 (あとは質問に答えるだけ)
```

---

# Gitによるチーム開発について

IssueとPull Request

Gitによるチーム開発は以下のような手順で行う

1. Issueをたてる(リーダー)
2. Issueを見て、ブランチを切って作業する(各自)
3. 作業用ブランチから`develop`ブランチにPull Requestを出す(各自)
4. Pull Requestを内容を確認しながらマージする(リーダー)

<br />

## Issueとは

日本語にすると「課題」  
ToDoリストのようなもの

---

## Pull Requestとは

作業しているブランチやリポジトリから、大元のブランチにマージするように依頼するリクエスト  
身内であっても、さらには自分自身でマージするときでも、コンフリクト対策のためにPull Requestは出すべき  
たいてい「プルリク」と略される

## マージとは

主にPull Requestの内容をもとのブランチに統合する作業

## コンフリクトとは

マージするときにマージ元とマージ先で噛み合わず、競合している状態

---
layout: end
---
# Git/GitHub研修(第2回)

Klef Project ・ Klef Lab  
Powered by <span class="text-red-400">[Slidev](https://ja.sli.dev) </span>
