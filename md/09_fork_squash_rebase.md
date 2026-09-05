# 第9章：発展 — Fork / upstream / Squash / Rebase

## この章のゴール

**基本編で避けた高度な運用を、何が違うか判断できる。**

# 1：Forkは「他人のrepoを自分側へ複製して開発する」仕組み

基本編では自分の練習repoを使ったため、`origin`だけで完結しました。

OSSなどのFork運用では、よく次の2つを使います。

```text
origin   → 自分のFork
upstream → 元のリポジトリ
```

追加例：

```bash
git remote add upstream https://github.com/OWNER/REPOSITORY.git
git remote -v
```

元repoの最新mainを取得：

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

## Create a merge commit

```text
feature commits ──┐
                  ├─ merge commit → main
main ─────────────┘
```

- branchの履歴を残す
- 初心者が構造を追いやすい

## Squash and merge

作業branchの複数commitを1つにまとめてmainへ入れます。

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
