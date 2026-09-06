# 第5章：fetch・merge・conflict

## この章のゴール

**GitHubの変更を取得し、自分のbranchへ統合し、conflictが出ても止まって判断できる。**

## `git pull`を分解する

`git pull`は、概念上おおむね次の2段階です。

```text
fetch
  ↓
integrate（merge / rebaseなど）
```

つまり、現在どのbranchにいるかを理解せずに実行すると、「どこへ何を統合したのか」が分かりにくくなります。

基本編では動きを見えるように分けます。

## GitHubの最新状態だけを取得する

```bash
git fetch origin
```

確認：

```bash
git log --oneline --graph --decorate --all --max-count=20
```

`origin/main`が進んでいても、自分の作業branchはまだ変わりません。

## 作業branchへmainの変更を取り込む

```bash
git switch feature/issue-12-add-profile
git status
git fetch origin
git merge origin/main
```

これで「GitHub上のmainの変更」を「現在の作業branch」へmergeします。

## conflictが出たら

まず止まります。

```bash
git status
```

競合ファイルには次のようなマーカーが入ります。

```text
<<<<<<< HEAD
現在のbranch側
=======
取り込もうとした側
>>>>>>> origin/main
```

やること：

1. 両方の意図を読む
2. 残す最終内容を決める
3. conflict markerを削除する
4. 保存する
5. `git add`する
6. `git commit`する

```bash
git add <解決したファイル>
git status
git commit -m "fix: コンフリクトを解消"
```

AIに解消を任せる場合も、両方の変更目的と期待する最終動作を渡します。「全部こちら側を採用」で片方の修正を消さないよう、解消後の差分と動作を確認してください。マーカーが消えただけでは、意味のある解決とは限りません。

## やり直したいとき

merge途中なら、条件が合えば次でmerge開始前へ戻せます。

```bash
git merge --abort
```

その後、状況を整理してから再実行します。

## `git pull --ff-only`はいつ使う？

`main`上で、自分がlocal mainへ独自commitしていない運用なら便利です。

```bash
git switch main
git pull --ff-only origin main
```

ただし基本編では、最初は `fetch` と `merge --ff-only` を分けて動きを確認します。

## 完了チェック

- [ ] `git fetch`だけでは作業ファイルが勝手にmergeされないと説明できる
- [ ] 作業branchへ `origin/main` をmergeできる
- [ ] conflict時に最初に `git status` を確認できる
- [ ] `git merge --abort`の用途を説明できる
- [ ] `git pull`が取得だけのコマンドではないと説明できる

---

前: [第4章](04_team_development_flow.md)  
次: [第6章 復旧](06_troubleshooting_and_recovery.md)

公式資料: https://git-scm.com/docs/git-pull
