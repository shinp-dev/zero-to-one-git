# 第7章：IssueからPRまでのハンズオン

## ゴール

`profiles/<ニックネーム>.md`を追加し、**Issue → Branch → Commit → Push → PR → Review → Merge** を完了する。

## 事前確認

- [ ] 自分専用の練習リポジトリを使っている
- [ ] GitHubへ認証できる
- [ ] `git status`が実行できる
- [ ] `origin`が自分の練習リポジトリを指している

```bash
git remote -v
git status
```

> [!IMPORTANT]
> 公開リポジトリでは、プロフィールに本名、学籍番号、個人メール、電話番号、住所などを書かないでください。ニックネームで構いません。

## Step 1：Issueを作る

GitHubのIssue template「プロフィール追加」を使います。

例：

```text
プロフィールを追加する：taro
```

Issue番号を控えます。以降は `#12` とします。

## Step 2：最新mainからbranchを作る

```bash
git switch main
git status
git fetch origin
git merge --ff-only origin/main
git switch -c feature/issue-12-add-profile
```

確認：

```bash
git branch --show-current
```

## Step 3：プロフィールを作る

`profile_template.md`をコピーし、例えば次へ保存します。

```text
profiles/taro.md
```

プレースホルダーを記入します。

## Step 4：差分を確認する

```bash
git status
git diff
```

プロフィール以外の変更が入っていないことを確認します。

## Step 5：stagingしてcommitする

```bash
git add profiles/taro.md
git diff --staged
git commit -m "feat: taroのプロフィールを追加"
```

## Step 6：pushする

```bash
git push -u origin feature/issue-12-add-profile
```

## Step 7：PRを作る

GitHubでPRを作り、次を確認します。

```text
base: main
compare: feature/issue-12-add-profile
```

PR templateを埋めます。

```markdown
## 変更内容
- taroのプロフィールを追加

## 確認内容
- [x] Issueの完了条件を満たした
- [x] 意図しないファイルを含んでいない
- [x] 個人情報や機密情報を含んでいない

Closes #12
```

## Step 8：レビュー対応

指摘があれば同じbranchで直します。

```bash
git add profiles/taro.md
git diff --staged
git commit -m "fix: プロフィールの記載漏れを修正"
git push
```

新しいPRは作りません。

## Step 9：Create a merge commitでマージする

基本編では **Create a merge commit** を選びます。

マージ後、`Closes #12`によりIssueが閉じたことを確認します。

## Step 10：ローカルを片付ける

```bash
git switch main
git fetch origin
git merge --ff-only origin/main
git branch -d feature/issue-12-add-profile
```

最後に履歴を見ます。

```bash
git log --oneline --graph --decorate --all --max-count=20
```

branchがmainへ合流した形を確認してください。

## 完了チェック

- [ ] Issueを作った
- [ ] 最新mainからbranchを作った
- [ ] `git diff --staged`を見てからcommitした
- [ ] PRのbase / compareを確認した
- [ ] 同じPRでレビュー修正した
- [ ] Create a merge commitで統合した
- [ ] Issueが閉じた
- [ ] local branchを削除した
- [ ] `git log --graph`で履歴を確認した

---

前: [第6章](06_troubleshooting_and_recovery.md)  
次: [第8章 conflict / revert演習](08_conflict_and_revert_practice.md)
