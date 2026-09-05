# 第0章：環境準備とGitHub認証

## この章のゴール

**Gitでcommitでき、GitHub CLI (`gh`) からGitHubを操作できる準備を整える。**

この教材では、次の2つを両方使います。

```text
Git  → 履歴・branch・commit・remote同期
 gh  → GitHub上のrepo・Issue・PR・Actionsなど
```

GitHubのWeb UIだけでも基本編は進められますが、**Gitと`gh`の役割の違いを知るため、GitHub CLIの導入を推奨**します。

## Step 1：GitとGitHub CLIを確認する

```bash
git --version
gh --version
```

Git for Windowsなど、現在サポートされている新しい版を使用してください。

`gh`が無い場合は、GitHub CLI公式サイトの案内に従って導入します。

- https://cli.github.com/

> [!NOTE]
> `git`と`gh`は別のコマンドです。`gh`を入れても、`git add`や`git commit`が不要になるわけではありません。

## Step 2：commitに記録する名前とメールを設定する

まず現在値を確認します。

```bash
git config --global user.name
git config --global user.email
```

未設定なら設定します。

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

GitHub上で個人メールアドレスを公開したくない場合は、GitHubが提供するnoreplyアドレスを利用できます。授業やチームの指定があればそちらを優先してください。

> [!NOTE]
> ここで設定するメールアドレスはcommitの作者情報です。GitHubへのログインパスワードではありません。

## Step 3：GitHubへ認証する

HTTPSを使う場合、GitHubは **GitHub CLI** または **Git Credential Manager (GCM)** の利用を案内しています。

### 方法A：GitHub CLI

```bash
gh auth login
```

HTTPSを選び、GitHubの認証情報をGitでも利用する設定にします。

確認：

```bash
gh auth status
```

`gh auth status`はGitHub CLIのログイン状態を確認します。

### 方法B：Git Credential Manager

Git for WindowsにはGCMが含まれています。HTTPSのcloneやpush時にブラウザ認証が表示されたら、GitHubへログインして許可します。

> [!IMPORTANT]
> GitHubアカウントのパスワードをGitのパスワード欄へ直接入力する方式は使いません。

## Step 4：練習用リポジトリを用意する

基本編は自分専用の練習リポジトリで行います。

教材がTemplate Repositoryとして設定されている場合：

1. GitHubで教材リポジトリを開く
2. **Use this template** を選ぶ
3. **Create a new repository** を選ぶ
4. 自分のアカウント配下へ練習用リポジトリを作る
5. 作成した自分のリポジトリをcloneする

cloneには2つの入口があります。

### Gitでclone

```bash
git clone https://github.com/<自分のユーザー名>/<練習リポジトリ名>.git
cd <練習リポジトリ名>
```

### `gh`でclone

```bash
gh repo clone <自分のユーザー名>/<練習リポジトリ名>
cd <練習リポジトリ名>
```

どちらも結果としてローカルにGitリポジトリができます。

違いは次の通りです。

```text
git clone
→ Gitそのものの機能。GitHub以外のGitサーバーにも使える

gh repo clone
→ GitHub向けの便利な入口。GitHub認証やOWNER/REPO表記と相性がよい
```

確認：

```bash
git remote -v
git status
gh repo view
```

- `origin` が **自分の練習リポジトリ** を指している
- `gh repo view` が同じGitHubリポジトリを表示する

この2つが確認できればOKです。

## Step 5：最初に覚える確認コマンド

### Gitの状態を見る

```bash
git status
git remote -v
git log --oneline --graph --decorate --all --max-count=20
```

### GitHubの状態を見る

```bash
gh auth status
gh repo view
gh pr status
```

`git`側は主にローカル履歴とremoteの状態、`gh`側はGitHubサービス上の状態を見る、と分けて考えます。

## 完了チェック

- [ ] `git --version` が表示される
- [ ] `gh --version` が表示される、またはWeb UIで進める方針を確認した
- [ ] `user.name` / `user.email` が設定されている
- [ ] GitHubへ認証できる
- [ ] 練習用リポジトリをcloneした
- [ ] `origin` が自分の練習リポジトリを指している
- [ ] `gh repo view`で同じリポジトリを確認できる
- [ ] `git`と`gh`の役割の違いを説明できる

---

次: [第1章 なぜGit/GitHubを使うか](01_why_git_and_github.md)

公式資料:
- https://docs.github.com/en/get-started/git-basics/set-up-git
- https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git
- https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository
- https://cli.github.com/manual/gh
- https://cli.github.com/manual/gh_repo_clone
- https://cli.github.com/manual/gh_auth_status
