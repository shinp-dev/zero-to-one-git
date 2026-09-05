# Git/GitHub チーム開発クイックガイド

## 10秒で見る全体像

```text
Issue → Branch → Edit → add → Commit → Push → PR → Review → Merge
```

## 今どこにいるか分からない

まずこれです。

```bash
git status
git branch --show-current
git log --oneline --graph --decorate --all --max-count=20
```

## 普段の開始

```bash
git switch main
git status
git fetch origin
git merge --ff-only origin/main
git switch -c feature/issue-12-short-name
```

## commitまで

```bash
git status
git diff
git add <file>
git diff --staged
git commit -m "説明"
```

## GitHubへ送る

```bash
git push -u origin <branch>
```

2回目以降：

```bash
git push
```

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

基本編はCreate a merge commitです。

```bash
git switch main
git fetch origin
git merge --ff-only origin/main
git branch -d <branch>
```

## 目的別

- [環境・認証](00_setup_and_auth.md)
- [Gitの地図](02_git_basic_concepts.md)
- [普段の開発フロー](04_team_development_flow.md)
- [fetch / conflict](05_sync_and_conflict.md)
- [復旧](06_troubleshooting_and_recovery.md)
- [PRハンズオン](07_hands_on_practice.md)
- [conflict / revert演習](08_conflict_and_revert_practice.md)
- [Fork / squash / rebase](09_fork_squash_rebase.md)
