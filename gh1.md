---
title: Git/GitHub研修(1)
file: klef-project/lecture/gh1.md
theme: klef
layout: cover
---

# Git/GitHub研修

Klef Project ・ Klef Lab  
Powered by [Slidev](https://ja.sli.dev)

---
transition: fade-out
---

# Gitとは

Linus Torvaldsが作った分散型バージョン管理システム

ファイルを <Hlt>いつ、だれが、どのように</Hlt> 変更したかを記録するシステム⇒ バージョン管理システム  
特にGitは <Hlt>デファクトスタンダード</Hlt> として広く使われている。

## Gitの特徴

<v-clicks>

- 分散型 → 万一データを保存しているサーバーが壊れても復元可能
- シェアが高い
- 情報が多い
- 複数の人が同時に編集することができる  
  ↑たまに同じところを変更したことによるエラー(コンフリクト)が起こるが、適切に対処可能

</v-clicks>

---

# GitHubとは

 
<Hlt>Git</Hlt> のホスティング環境  

**Git**のログやファイルを保管・共有するためのシステム。  
GitHubがトップシェアではあるが、GitLabにも一定の人気がある。

## GitHubの特徴

<v-clicks>

- デファクトスタンダードとして広く使われている
- 情報が多い
- Microsoft傘下のためVSCodeとの相性がいい
- 学校でもよく使われる

</v-clicks>


---

# 用語について

<v-clicks>

- リポジトリ：Gitでファイルを管理するときの管理対象のディレクトリのこと。
- ディレクトリ：Unix系システムにおけるフォルダーの別名。
- Unix系システム：(主に)MacとLinux。
- Linux：Linus Torvaldsが作ったOS。オープンソースで公開。
- Debian GNU/Linux：Linuxディストリビューションの1つ。
- Linuxディストリビューション：Linuxに様々なソフトをつけてインストールしてそのまま使えるようにしたもの。
- Ubuntu：Debian GNU/Linuxをベースとしたディストロ。
- ディストロ：Linuxディストリビューションの略称。
- RedHat Enterprise Linux (RHEL)：商用のディストロ。
- Arch Linux： 「シンプルさ」に重しをおいたディストロ。
- NixOS：Nixパッケージマネージャーを中心としたディストロ。

</v-clicks>

---

# Windows PowerShellとGit Bash

Windowsのターミナル環境

### Windows PowerShellとは

- Windowsのデフォルトのシェル
- Bash**非互換**
- Unix系コマンドのエイリアスは用意されてる
- コマンド名がそのまますぎる

### Git Bashとは

- Gitをインストールするとついてくる
- Bash互換
- **Unix系コマンドがそのまま使える**
- 実際は「MSYS2」上で動作

情報通信課で使用するコマンドは基本的にPowerShellでも動くため**特にシェルは指定しない**  
~~担当者はrmコマンドのオプションをつけようとしたらPowerShellに怒られました~~

---

# Git/GitHubのセットアップ

Git/GitHubを使うには、以下の手順を踏む必要がある。

1. Gitのインストール
2. GitHubアカウント作成
3. Gitの初期設定

---

# Gitのインストール

## (A)インストーラーでインストール

1. [https://git-scm.com](https://git-scm.com)からインストーラーをDL
2. DLしたインストーラーを開く
3. インストーラーに沿ってインストール

<br />

## (B)Wingetでインストール

1. Wingetが入っていることを確認 `winget -v`
2. 以下のコマンドを実行
   ```ps
   winget install -id Git.Git
   ```

---

# Gitの設定

git config

`git config`コマンドには以下の3つのスコープがある
- system
- global
- local

ただし`system`は基本的に使わない

今回は`global`を使用

```bash
git config --global init.defaultBranch main
git config --global core.autocrlf input
git config --global user.email < Your EMail >
git config --global user.name < Your User name >
```

< Your Email >< Your User Name >にはそれぞれ自分のメールアドレスと名前を入力
ここで入力した情報はあとでGitHubアカウントの作成のときに用いるため、控えておくこと。

---

# リポジトリの初期化

git init

現在のディレクトリ(<Hlt>カレントディレクトリ</Hlt>)でGitによるバージョン管理を有効にする  
＝<Hlt>リポジトリを初期化する</Hlt>　or 既存のプロジェクトをGitリポジトリに変換する

その時に使うコマンドが<Hlt>`git init`</Hlt>

## 使用例
```bash
mkdir test
cd test
git init
```

`git init`に引数は与えなくてよい  


---

# GitHubのアカウント作成

GitHubアカウントの作成は、Webページに沿って必要な情報を入力するだけでできる。  
GitHubのURL: <span class="text-sky-500">[https://github.com](https://github.com) </span>

### 作成手順

<v-clicks>

1. 右上の`Sign Up`をクリック
2. `Enter your Email`と聞かれるので<Hlt>Gitに設定した</Hlt>メールアドレスを入力し、`Continue`。
3. `Create Password`と聞かれるので、パスワードを作成する。
4. `Enter a Username`と聞かれるので、<Hlt>Gitに設定した</Hlt>ハンドルネームを入力する。
5. `Email preferences`で`Receive occasional product updates and announcements.`と聞かれるので、どちらか選択して`Continue`。
6. `Verify your Account`と聞かれるので、`認証する`を押して人間であることを認証する。
7. `You're almost done! we sent a launch code to ~`と表示されるので、メールを確認し、そこに書かれているコードを入力する。

</v-clicks>

---

# 新規リポジトリの作成

GitHubリポジトリの新規作成

1. GitHubにサインイン
2. 左の方にある`New`をクリック
3. 真ん中の方の`Repository Name`だけ埋めて(ここでは"test")`Create Repository`

![新規リポジトリの作成](gh1/new_repo.png)

---

# ローカルとGitHubの関連付け

git remote

手元の環境→Local ネットワーク上の環境(GitHubなど)→Remote

1. GitHubのリポジトリページに移動
2. "Quick Setup"欄にあるURLをコピー

![GitHub](gh1/remote_setting.png)

---

## ローカルとリモートの関連付け(P.2)

3. 関連付けたいリポジトリのルートへ移動→PowerShellを開く  
※ルート：そのプロジェクトの最上層のフォルダ、すなわちそのプロジェクトのファイルがまとめられているフォルダ
4. 以下のコマンドを入力

```bash
git remote add origin https://github.com/~
```

このURLは先ほどコピーしたもの

ここでは、先ほどGitHubで作成したリポジトリを`origin`という名前で参照できるように登録した。  
別に他の名称でもいいが、慣習的に`origin`が使われるため、特段の理由がない限り`origin`を使用する。

---

# 次回予告

- Gitでファイルを管理してみよう
- Gitの様々なコマンド
- GitHub CLI

---
layout: end
---

# Git/GitHub研修

Klef Project ・ Klef Lab  
Powered by [Slidev](https://ja.sli.dev)