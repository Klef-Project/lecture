---
title: Git/GitHub研修(1)
theme: purplin
layout: quote
---

# GitHub研修

2024年度学友会執行部情報通信課  
Powerd by <span class="text-red-400">[Slidev](https://ja.sli.dev) </span>

<Bottom></Bottom>

---
# Gitとは

Linus Torvaldsが作った分散型バージョン管理システム

ファイルを <span class="text-red-400"> いつ、だれが、どのように </span> 変更したかを記録するシステム⇒ バージョン管理システム  
特にGitは <span class="text-red-400">デファクトスタンダード </span> として広く使われている。

## Gitの特徴

<v-clicks>

- 分散型 → 万一データを保存しているサーバーが壊れても復元可能
- シェアが高い
- 情報が多い
- 複数の人が同時に編集することができる  
  ↑たまに同じところを変更したことによるエラー(コンフリクト)が起こるが、適切に対処可能

</v-clicks>
<Bottom></Bottom>

---

# GitHubとは

 
<span class="text-red-500"> **Git** </span> のホスティング環境  

**Git**(後述)のログやファイルを保管・共有するためのシステム。  
GitHubがトップシェアではあるが、GitLabにも一定の人気がある。

## GitHubの特徴

<v-clicks>

- デファクトスタンダードとして広く使われている
- 情報が多い
- Microsoft傘下のためVSCodeとの相性がいい
- 「総合工学システム実験実習」テーマ「I1」でも扱う

</v-clicks>

<Bottom></Bottom>



---

# Git/GitHubのセットアップ

2023年度知能情報コース2年「プログラミング1」第14\~16回講義資料による

Git/GitHubを使うには、以下の手順を踏む必要がある。

1. GitHubアカウント作成
2. Gitのインストール
3. Gitの初期設定

<Bottom></Bottom>

---

## GitHubのアカウント作成

GitHubアカウントの作成は、Webページに沿って必要な情報を入力するだけでできる。  
GitHubのURL: <span class="text-sky-500">[https://github.com](https://github.com) </span>

### 作成手順

1. 右上の`Sign Up`をクリック
2. `Enter your Email`(Eメールを入力してください)と聞かれるのでメールアドレスを入力し、`Continue`。
3. `Create Password`(パスワードを作成してください)と聞かれるので、パスワードを作成する。
4. `Enter a Username`と聞かれるので、<span class="text-red-600 border-1 border-red-600 border-double">**本名以外の**</span>ハンドルネームを入力する。
5. `Email preferences`で`Receive occasional product updates and announcements.`(時々、製品のアップデートなどの情報を取得しますか(=メールマガジンを購読しますか))と聞かれるので、どちらか選択して`Continue`。
6. `Verify your Account`と聞かれるので、`認証する`を押して人間であることを認証する。
7. `You're almost done! we sent a launch code to ~`(もう少しで終わりです! \~に認証コードを送りました。)と表示されるので、メールを確認し、そこに書かれているコードを入力する。

<Bottom></Bottom>

---
layout: image
src: "../public/gh1/fig001.png"
---

<Bottom></Bottom>

---

## Gitのインストール

基本的にインストーラー通りにインストールする。  
GitのHPのURL:  <span class="text-sky-500">[https://git-scm.com](https://git-scm.com) </span>

### インストール手順

0. `ターミナル`で`git -v`を実行して、エラーになることを確認する。
1. GitのHPからインストーラーをDLする。
2. インストーラーを実行する。
3. `Select Components`のところで、`Add a Git Bash Profile to Windows Terminal`にチェックを入れる。
4. `Adjusting the name of the initial branch in new repositories`で`Override the default branch name for new repositories`を選択する。
5. `Configuring the line encoding conversions`を`Checkout as-is, commit Unix-style line encoding`を選択する。
6. `ターミナル`で`git -v`を実行して、数値が出力されることを確認する。

※特筆していない設定については基本的にデフォルトで問題ないが、好みに応じて変更して構わない。

<Bottom></Bottom>

---

### 推奨設定への変更方法

インストール済みの人向け

1. ターミナルで以下のコマンドを実行する。

```
git config --global init.defaultBranch main
git config --global core.autoinput input
```

2. ターミナルで「設定」を開き、その中の設定マークを押し、`JSONファイルを開く`
3. スタートメニューの`Git`>`Git Bash`を右クリックし、`詳細`>`ファイルの場所を開く`
4. `Git Bash`のショートカットを右クリックして`プロパティ`を開く
5. `リンク先`をコピー

<Bottom></Bottom>

---

#### 推奨設定への変更方法(p.2)

6. ターミナルで`guid::NewGuid()`を実行する。
7. JSONファイルに戻り、以下のように書く。

```json {3,7-11|7-11}
{
    ...
    "list": [
        {
            ...
        },
        {
            "name": "Git Bash",
            "commandline": "(先ほどコピーしたGit Bashのパス)",
            "guid": "([guid]:NewGuid()で生成された一意の文字列)"
        }
    ],
    ...
}
```

<Bottom></Bottom>

---

## Gitの初期設定

以下の手順に沿って行う。

1. GitHubにアクセスし、ユーザー名を控える
2. GitHubの自分のアイコンをクリックし、`Your Profile`を選択
3. メールアイコンのところのメールアドレスを控える
4. 以下のコマンドを実行する

```
git config --global user.email <GitHubメールアドレス>
git config --global user.name <GitHubユーザー名>
```

<Bottom></Bottom>

---

# Git/GitHubを使ってみよう

実際にリポジトリをフォークしてクローン、一部変更の上でコミット・プッシュを行う。

1. [https://github.com/haru-0205/github-traning](https://github.com/haru-0205/github-traning)にアクセス
2. `Fork`を選択
3. `Create a new fork`が表示されたら、`Owner`のドロップダウンリストから自分のアカウントを選択
4. `Create fork`
5. `git clone https://github.com/<GitHub ユーザー名>/github-traning.git`を実行
6. `code github-traning.git`を実行
7. VSCodeで`README.md`を適当に編集
8. `Ctrl`+`@`でターミナルを開き、`git add .`を実行
9. `git commit -m "README.mdを編集"`を実行
10. `git push`を実行

<Bottom></Bottom>
