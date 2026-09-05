# 第9章：発展 — Fork / upstream / Squash / Rebase

## この章のゴール

**基本編で避けた高度な運用を、何が違うか判断できる。さらに、Fork操作もWeb UIと`gh`の両方から行えることを知る。**

# 1：Forkは「他人のrepoを自分側へ複製して開発する」仕組み

基本編では自分の練習repoを使ったため、`origin`だけで完結しました。

OSSなどのFork運用では、よく次の2つを使います。

```text
origin   → 自分のFork
upstream → 元のリポジトリ
```

## Web UIでFork

GitHub上で対象repoの **Fork** を選び、自分のアカウントへForkを作ります。

その後、自分のForkをcloneし、元repoを`upstream`へ追加します。

```bash
git clone https://github.com/<自分>/<fork名>.git
cd <fork名>
git remote add upstream https://github.com/OWNER/REPOSITORY.git
git remote -v
```

## `gh`でFork

GitHub CLIなら、Fork作成とcloneをまとめられます。

```bash
gh repo fork OWNER/REPOSITORY --clone
```

`gh repo fork`はForkを作成し、構成に応じて`origin` / `upstream` remoteの設定も補助します。

Fork済みrepoを`gh repo clone`でcloneした場合も、親repoを`upstream`として追加する機能があります。

```bash
gh repo clone <自分>/<fork名>
git remote -v
```

> [!NOTE]
> `gh`がremote設定を自動化しても、最終的には`git remote -v`で実際の向き先を確認してください。

## 元repoの最新mainを取得

ここからはGitの操作です。

```bash
git fetch upstream
git switch main
git merge --ff-only upstream/main
```

必要なら自分のForkへ反映：

```bash
git push origin main
```

Fork環境で `git pull origin main` とだけ覚えると、元repoではなく自分のForkを更新対象にしてしまうため、`origin` / `upstream`を区別します。

# 2：PRのmerge方式

GitHub Web UIでも`gh pr merge`でも、merge方式を選べます。

## Create a merge commit

```text
feature commits ──┐
                  ├─ merge commit → main
main ─────────────┘
```

- branchの履歴を残す
- 初心者が構造を追いやすい

Web UIでは **Create a merge commit**、CLIでは次です。

```bash
gh pr merge --merge
```

## Squash and merge

作業branchの複数commitを1つにまとめてmainへ入れます。

```bash
gh pr merge --squash
```

- mainの履歴を簡潔にしやすい
- 元branchのcommit IDはmainにそのまま入らない
- merge後にlocal `git branch -d`が「未merge」と判断する場合がある

その場合は、**mainへ目的の変更が入ったことを確認してから**不要branchを削除します。

```bash
git branch -D <branch>
```

`-D`は強制削除なので、確認なしに使いません。

## Rebase and merge

作業branchのcommitをmainの先へ並べ直すように統合します。

```bash
gh pr merge --rebase
```

- 直線的な履歴になりやすい
- commit IDが変わることがある
- 履歴書き換えの理解が必要

# 3：作業branchでのrebase

チームによっては次の運用を使います。

```bash
git fetch origin
git rebase origin/main
```

rebaseは自分のcommitを別の土台へ載せ直すため、共有済みbranchで使うと他人へ影響します。

基本編ではmergeを使い、rebaseはチームのルールが決まっている場合に使ってください。

## `git`と`gh`の使い分けをもう一度整理

```text
ForkをGitHub上に作る
→ Web UI または gh repo fork

remoteを確認・fetch・mergeする
→ Git

GitHub上のPRをmergeする
→ Web UI または gh pr merge
```

`gh`がGitHub操作を便利にしても、ローカルGitの履歴やremoteの意味は変わりません。

## 最終判断

```text
まず安全に理解したい
→ merge

mainの履歴をPR単位で1commitにしたい
→ squash

直線的なcommit履歴を維持したい
→ rebase
```

どれが絶対に正しいという話ではありません。**チームで方式を決め、混在させないこと**が重要です。

---

前: [第8章](08_conflict_and_revert_practice.md)  
[クイックガイド](git_team_development_guide.md)

公式資料:
- https://cli.github.com/manual/gh_repo_fork
- https://cli.github.com/manual/gh_repo_clone
- https://cli.github.com/manual/gh_pr_merge
