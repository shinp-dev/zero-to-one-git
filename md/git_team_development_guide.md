# Git/GitHub チーム開発クイックガイド

## 10秒で見る全体像

```text
Issue → Branch → Edit → add → Commit → Push → PR → Review → Merge
```

## Git / GitHub / `gh` の役割

| 何をする？ | 主に使うもの |
|---|---|
| 差分・staging・commit・branch・fetch・merge | Git |
| Issue・PR・Review・Actionsなど | GitHub |
| GitHubをターミナルから操作 | `gh` |

```text
Web UI  ←→  GitHub service  ←→  gh
                    ↑
                 git push
                    ↑
                 local Git
```

`gh`はGitHub操作のCLIで、`git add`や`git commit`の代わりではありません。

## 今どこにいるか分からない

### Git

```bash
git status
git branch --show-current
git log --oneline --graph --decorate --all --max-count=20
```

### GitHub

```bash
gh auth status
gh repo view
gh pr status
```

## clone

Gitで：

```bash
git clone https://github.com/OWNER/REPO.git
```

GitHub CLIで：

```bash
gh repo clone OWNER/REPO
```

## Issue

Web UIでも`gh`でも同じIssueを操作します。

```bash
gh issue list
gh issue create
gh issue view <番号>
```

## 普段の開始

最初の`git status`で未commit変更がある場合は、現在の作業をcommitするか退避方針を決めてから、branchを切り替えます。

```bash
git status
git switch main
git fetch origin
git merge --ff-only origin/main
git switch -c feature/issue-12-short-name
```

Issueとbranch作成を`gh`でまとめる発展的な例：

```bash
gh issue develop 12 --checkout --base main --name feature/issue-12-short-name
```

## commitまで

```bash
git status
git diff
git add <file>
git diff --staged
git commit -m "説明"
```

ここはGitの仕事です。

## GitHubへ送る

```bash
git push -u origin <branch>
```

2回目以降：

```bash
git push
```

## PR

作成：

```bash
gh pr create --base main
```

確認：

```bash
gh pr status
gh pr view
gh pr checks
```

基本編のmerge commit：

```bash
gh pr merge --merge
```

すべてGitHub Web UIからも同じ操作ができます。

## AIが作業を終えたら

作業branchで確認します。

```bash
git status
git diff
git diff --staged
git fetch origin
git diff --stat origin/main...HEAD
git diff origin/main...HEAD
```

`status`がcleanでもcommit済みの変更は残っています。未追跡ファイルは開いて確認します。PR作成後はFiles changedまたは`gh pr diff`で提出差分を確認し、完了条件と検証結果を照合します。

依頼例と並行作業の注意は [第10章](10_ai_assisted_development.md) へ。

## mainの変更を作業branchへ取り込む

```bash
git fetch origin
git merge origin/main
```

conflict時：

```bash
git status
```

やめるなら：

```bash
git merge --abort
```

## 戻したい

| 状況 | 操作 |
|---|---|
| 未commit編集を捨てる | `git restore <file>` |
| addを取り消す | `git restore --staged <file>` |
| 未pushの直前commitを戻す | `git reset HEAD~1` |
| 共有済みcommitを打ち消す | `git revert <commit>` |

> [!WARNING]
> `reset --hard` / force pushは、意味と影響範囲が分からない状態では使いません。

## PRマージ後

GitHub上でmergeした後、ローカルGitを更新します。

```bash
git switch main
git fetch origin
git merge --ff-only origin/main
git branch -d <branch>
```

## Fork

Web UIでもできますが、`gh`ならFork作成とcloneをまとめられます。

```bash
gh repo fork OWNER/REPO --clone
```

確認はGitで行います。

```bash
git remote -v
```

## 目的別

- [環境・認証](00_setup_and_auth.md)
- [Gitの地図](02_git_basic_concepts.md)
- [Issueとbranch](03_issue_and_branch.md)
- [普段の開発フロー](04_team_development_flow.md)
- [fetch / conflict](05_sync_and_conflict.md)
- [復旧](06_troubleshooting_and_recovery.md)
- [PRハンズオン](07_hands_on_practice.md)
- [conflict / revert演習](08_conflict_and_revert_practice.md)
- [Fork / squash / rebase](09_fork_squash_rebase.md)
- [AIと進める開発](10_ai_assisted_development.md)

GitHub CLI公式: https://cli.github.com/manual/
