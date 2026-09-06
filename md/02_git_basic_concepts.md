# 第2章：Gitの地図 — Worktree / Staging / Commit / Branch / HEAD

## この章のゴール

**Gitの操作で「何がどこへ動くか」を図で説明できる。**

## まず全体を見る

```text
編集中のファイル
Worktree
   │ git add
   v
次のcommitに入れる変更
Staging area / Index
   │ git commit
   v
ローカルの履歴
Commit
   │ git push
   v
GitHub上の履歴
origin/<branch>
```

## Stagingは何のため？

Stagingは、**次の1回のcommitへ入れる変更範囲を選ぶ場所**です。

例えば同じ作業中にREADMEと設定ファイルを触っていても、READMEだけを先にcommitできます。

```bash
git status
git diff
git add README.md
git diff --staged
git commit -m "docs: READMEを更新"
```

- `git diff` → まだstagingしていない変更
- `git diff --staged` → 次のcommitに入る変更

未追跡の新規ファイルは`git status`で見つけ、ファイルを開くか、対象をaddした後の`git diff --staged`で中身を確認します。commit後はこの2つのdiffから変更が消えます。直前のcommitは`git show HEAD`、作業branch全体は`git fetch origin`後の`git diff origin/main...HEAD`で確認できます。

## Commitは「その時点の記録」

```text
A ← B ← C
```

各commitは、それまでの履歴につながっています。

```bash
git log --oneline --graph --decorate --all --max-count=20
```

実際の履歴を図として確認してください。

## Branchは「別フォルダ」ではない

初心者向けには「作業を分ける場所」と考えて構いませんが、Git内部ではbranchは**あるcommitを指す名前**です。

```text
A ← B ← C
        ↑   ↑
      main  feature/login
```

作業ブランチでcommitすると、そのbranchが新しいcommitを指すようになります。

## HEADは「今いる場所」

通常、`HEAD`は現在checkout / switchしているbranchを指します。

```text
A ← B ← C
        ↑   ↑
      main  feature/login
             ↑
            HEAD
```

確認：

```bash
git status
git branch --show-current
```

`HEAD~1` は「現在のcommitの1つ前」を表します。第6章の復旧で出てくるため、ここで意味だけ覚えてください。

## `origin/main`は何？

cloneすると通常、clone元のリモートに `origin` という名前が付きます。

```text
main          → 自分のPC上のmain
origin/main   → 最後に取得したGitHub側mainの位置
```

GitHubの最新状態をPCへ取得する操作が `git fetch` です。

```bash
git fetch origin
```

これだけでは、自分の `main` や作業ファイルは勝手に書き換わりません。

## 状態を見る3コマンド

```bash
git status
git diff
git log --oneline --graph --decorate --all --max-count=20
```

迷ったら変更系コマンドより先に、この3つで状況を見ます。

## 完了チェック

- [ ] Worktree / Staging / Commitの順を説明できる
- [ ] `git add`が「GitHubへ送る操作」ではないと説明できる
- [ ] branchとHEADの関係を説明できる
- [ ] `main`と`origin/main`の違いを説明できる
- [ ] `git diff`と`git diff --staged`を使い分けられる

---

前: [第1章](01_why_git_and_github.md)  
次: [第3章 IssueとBranch](03_issue_and_branch.md)
