# 第8章：conflictとrevertをわざと起こす

## この章のゴール

**正常系だけでなく、失敗を自分で観察して復旧できる。**

この章は練習用リポジトリで行ってください。

# Part A：conflictを作る

## Step 1：練習ファイルを作るbranch A

```bash
git switch main
git switch -c practice/conflict-a
```

`conflict-practice.txt`を作り、次の1行を書きます。

```text
好きな言語: TypeScript
```

```bash
git add conflict-practice.txt
git commit -m "test: conflict練習A"
```

## Step 2：mainからbranch Bを作る

```bash
git switch main
git switch -c practice/conflict-b
```

同じファイルを作り、同じ行へ別内容を書きます。

```text
好きな言語: Python
```

```bash
git add conflict-practice.txt
git commit -m "test: conflict練習B"
```

## Step 3：Aをmainへmergeする

```bash
git switch main
git merge practice/conflict-a
```

## Step 4：Bもmergeしてconflictを起こす

```bash
git merge practice/conflict-b
```

ここでは失敗が正解です。

```bash
git status
```

競合ファイルを開き、最終的な内容を自分で決めます。例えば：

```text
好きな言語: TypeScript / Python
```

markerを消して保存します。

```bash
git add conflict-practice.txt
git status
git commit -m "test: conflictを解消"
```

履歴を確認：

```bash
git log --oneline --graph --decorate --all --max-count=20
```

# Part B：revertを体験する

## Step 1：取り消したくなるcommitを作る

```bash
git switch -c practice/revert
```

`revert-practice.txt`を作ります。

```text
この変更は後で取り消します
```

```bash
git add revert-practice.txt
git commit -m "test: revert対象を追加"
```

## Step 2：commitを消さずに打ち消す

```bash
git revert HEAD
```

エディタが開いた場合はcommit messageを確認して保存します。

確認：

```bash
git log --oneline --decorate --max-count=5
```

元のcommitとRevert commitの両方が履歴へ残ります。

```text
変更した事実
  ↓
間違いだったので戻した事実
```

これが共有履歴で `revert` が安全な理由です。

## 完了チェック

- [ ] conflictを意図的に発生させた
- [ ] `git status`から競合ファイルを特定した
- [ ] markerを消してmergeを完了した
- [ ] `git revert HEAD`で取り消し用commitを作った
- [ ] resetとrevertの違いを履歴で確認した

---

前: [第7章](07_hands_on_practice.md)  
次: [第9章 Fork / squash / rebase](09_fork_squash_rebase.md)
