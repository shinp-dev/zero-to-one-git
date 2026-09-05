# 第0章：環境準備とGitHub認証

## この章のゴール

**Gitでcommitでき、GitHubへpushできる準備を整える。**

## Step 1：Gitを確認する

```bash
git --version
```

Git for Windowsなど、現在サポートされている新しい版を使用してください。

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

GitHub CLIを導入済みなら次を実行します。

```bash
gh auth login
```

HTTPSを選び、GitHubの認証情報をGitでも利用する設定にします。

確認：

```bash
gh auth status
```

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

```bash
git clone https://github.com/<自分のユーザー名>/<練習リポジトリ名>.git
cd <練習リポジトリ名>
```

確認：

```bash
git remote -v
git status
```

`origin` が **自分の練習リポジトリ** を指していればOKです。

## Step 5：最初に覚える確認コマンド

```bash
git status
git remote -v
git log --oneline --graph --decorate --all --max-count=20
```

この3つは「壊すためのコマンド」ではなく、**今の状態を見るコマンド**です。

## 完了チェック

- [ ] `git --version` が表示される
- [ ] `user.name` / `user.email` が設定されている
- [ ] GitHubへ認証できる
- [ ] 練習用リポジトリをcloneした
- [ ] `origin` が自分の練習リポジトリを指している

---

次: [第1章 なぜGit/GitHubを使うか](01_why_git_and_github.md)

公式資料:
- https://docs.github.com/en/get-started/git-basics/set-up-git
- https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git
- https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository
