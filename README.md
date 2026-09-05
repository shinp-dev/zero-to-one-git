# Zero to One: Git / GitHub チーム開発

Gitを初めて使う人が、**「コマンドを暗記する」のではなく、今どこにいて何を動かしているかを理解しながら**、Issue → Branch → Commit → Pull Request → Review → Merge を一周するための日本語教材です。

## この教材で一番大事な地図

```text
Issue（何をするか）
  ↓
Branch（作業を分ける）
  ↓
Worktree（編集する）
  ↓ git add
Staging（次のcommitに入れる変更を選ぶ）
  ↓ git commit
Local repository（履歴として記録する）
  ↓ git push
GitHub / Pull Request（共有・レビュー）
  ↓ Merge
main（確認済みの変更を統合）
```

## 対象

- Gitを初めて使う人
- 個人開発からチーム開発へ進む人
- GitHubを使う授業・卒業制作・開発チームへ参加する人
- AIにGit操作を任せる場合でも、状態と差分を自分で確認できるようになりたい人

前提は、ファイル操作とターミナルの基本だけです。

## 学習順序

| 章 | テーマ | ゴール |
|---|---|---|
| [0](md/00_setup_and_auth.md) | 環境準備・GitHub認証 | commit / pushできる環境を作る |
| [1](md/01_why_git_and_github.md) | なぜGit/GitHubを使うか | Issue・Branch・PRの目的を説明できる |
| [2](md/02_git_basic_concepts.md) | Gitの地図 | Worktree / Staging / Commit / Branch / HEADを説明できる |
| [3](md/03_issue_and_branch.md) | IssueとBranch | 1つの目的に1つの作業ブランチを作れる |
| [4](md/04_team_development_flow.md) | 普段の開発フロー | IssueからMergeまで進められる |
| [5](md/05_sync_and_conflict.md) | fetch・merge・conflict | リモートとの差と競合を安全に扱える |
| [6](md/06_troubleshooting_and_recovery.md) | 復旧 | 状況に応じてrestore / reset / revertを選べる |
| [7](md/07_hands_on_practice.md) | PRハンズオン | プロフィール追加をPRで完了できる |
| [8](md/08_conflict_and_revert_practice.md) | conflict / revert演習 | 意図的な失敗から自力で戻せる |
| [9](md/09_fork_squash_rebase.md) | 発展 | Fork / upstream / squash / rebaseを区別できる |

迷ったら [クイックガイド](md/git_team_development_guide.md) を開いてください。

## ハンズオンの始め方

基本編は、**自分専用の練習リポジトリ**で行う前提です。教材管理者がこのリポジトリをTemplate Repositoryとして設定している場合は、GitHubの **Use this template** から自分のリポジトリを作成してください。

Templateが使えない環境では、授業担当者が用意した練習リポジトリを使用してください。Forkは基本編では使わず、第9章で扱います。

> [!IMPORTANT]
> 公開リポジトリのプロフィール演習では、本名である必要はありません。学籍番号、個人メールアドレス、電話番号、住所などの個人情報は書かないでください。

## 基本編のルール

- 作業前と迷ったときは `git status`
- `main`へ直接作業しない
- 1つのIssueに対して1つの作業ブランチ
- commit前に `git diff --staged`
- 基本編のPRは **Create a merge commit** で統合する
- 共有済みのcommitを取り消すときは、原則 `git revert`
- `reset --hard` と force push は、意味が分からない状態では実行しない

## 公式資料

- GitHub: Gitのセットアップと認証  
  https://docs.github.com/en/get-started/git-basics/set-up-git
- GitHub: GitHub CLI / Git Credential Manager  
  https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git
- GitHub: Template Repository  
  https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository
- Git: `git pull`  
  https://git-scm.com/docs/git-pull
- Git: `git revert`  
  https://git-scm.com/docs/git-revert
- Git: `git reset`  
  https://git-scm.com/docs/git-reset

## リポジトリ管理者向け

教材リポジトリ自身の推奨設定は [REPOSITORY_SETTINGS.md](REPOSITORY_SETTINGS.md) にまとめています。

## License

[MIT License](LICENSE)
