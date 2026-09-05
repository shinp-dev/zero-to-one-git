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

## Git / GitHub / `gh` は何が違う？

| 名前 | 役割 | 代表例 |
|---|---|---|
| **Git** | 変更履歴・branch・commit・remoteとの同期を扱う仕組み | `git status`, `git add`, `git commit`, `git fetch`, `git merge` |
| **GitHub** | Gitの履歴を共有し、Issue・PR・Review・Actionsなどで協働するサービス | GitHub Web UI |
| **`gh`** | GitHubをターミナルから操作する公式CLI | `gh issue`, `gh pr`, `gh repo`, `gh run` |

`gh`はGitを置き換えるものではありません。例えば、編集した変更をstagingしてcommitするのはGitの仕事です。一方、IssueやPRを作る、PRの状態を見る、GitHub上でmergeする、といった操作はWeb UIでも`gh`でもできます。

一部は同じ結果へ別の入口があります。

| やりたいこと | Git / Web UI | `gh` |
|---|---|---|
| GitHub repoをclone | `git clone <URL>` | `gh repo clone OWNER/REPO` |
| Issueを作る | GitHubのIssues画面 | `gh issue create` |
| Issueを見る | GitHubのIssue画面 | `gh issue view <番号>` |
| PRを作る | GitHubのPull requests画面 | `gh pr create` |
| PRの状態を見る | GitHubのPR画面 | `gh pr status`, `gh pr checks` |
| PRをmerge | GitHubのMergeボタン | `gh pr merge --merge` |

この教材では、**まずGitとWeb UIで仕組みを理解し、その直後に同じGitHub操作を`gh`でも確認する**進め方にします。

## 対象

- Gitを初めて使う人
- 個人開発からチーム開発へ進む人
- GitHubを使う授業・卒業制作・開発チームへ参加する人
- AIにGit操作を任せる場合でも、状態と差分を自分で確認できるようになりたい人

前提は、ファイル操作とターミナルの基本だけです。

## 学習順序

| 章 | テーマ | ゴール |
|---|---|---|
| [0](md/00_setup_and_auth.md) | 環境準備・GitHub認証 | Gitと`gh`を使える環境を作る |
| [1](md/01_why_git_and_github.md) | なぜGit/GitHubを使うか | Git / GitHub / `gh`の役割を説明できる |
| [2](md/02_git_basic_concepts.md) | Gitの地図 | Worktree / Staging / Commit / Branch / HEADを説明できる |
| [3](md/03_issue_and_branch.md) | IssueとBranch | IssueをWeb/`gh`で扱い、作業ブランチを作れる |
| [4](md/04_team_development_flow.md) | 普段の開発フロー | IssueからMergeまで進められる |
| [5](md/05_sync_and_conflict.md) | fetch・merge・conflict | リモートとの差と競合を安全に扱える |
| [6](md/06_troubleshooting_and_recovery.md) | 復旧 | 状況に応じてrestore / reset / revertを選べる |
| [7](md/07_hands_on_practice.md) | PRハンズオン | Web UIと`gh`の両方でGitHub上の状態を確認できる |
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
- GitHub上の操作は、Web UIと`gh`のどちらでも同じ対象を操作していることを意識する
- 基本編のPRは **Create a merge commit** で統合する
- 共有済みのcommitを取り消すときは、原則 `git revert`
- `reset --hard` と force push は、意味が分からない状態では実行しない

## AIを使う場合

AIにGit操作やコード修正を依頼しても構いません。ただし、実行前後に人間が最低限次を確認します。

```bash
git status
git branch --show-current
git diff
git diff --staged
gh pr status
```

`gh pr status`は、現在のbranchに関係するPRやレビュー状態を確認するのに使えます。

特にAIから `reset --hard`、force push、大量ファイル削除、別branchへの切り替えを提案された場合は、**何が失われるか説明できるまで実行しない**ことを基本にします。

AIが操作した場合でも、最終的に次を説明できる状態が目標です。

- 今どのbranchにいるか
- どのファイルが変更されたか
- 次のcommitに何が入るか
- GitHubへ何をpushするか
- PRがどのIssueを解決するか
- Web UIと`gh`が同じIssue / PRを操作していること

## 公式資料

- GitHub: Gitのセットアップと認証  
  https://docs.github.com/en/get-started/git-basics/set-up-git
- GitHub: GitHub CLI / Git Credential Manager  
  https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git
- GitHub CLI manual  
  https://cli.github.com/manual/
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
