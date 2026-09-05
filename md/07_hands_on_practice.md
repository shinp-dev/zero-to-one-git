# 第7章：IssueからPRまでのハンズオン

## ゴール

`profiles/<ニックネーム>.md`を追加し、**Issue → Branch → Commit → Push → PR → Review → Merge** を完了する。

さらに、GitHub上のIssue / PRを **Web UIと`gh`の両方から確認できる**状態を目指します。

## 事前確認

- [ ] 自分専用の練習リポジトリを使っている
- [ ] GitHubへ認証できる
- [ ] `git status`が実行できる
- [ ] `gh auth status`が成功する、またはWeb UIで進める方針を確認した
- [ ] `origin`が自分の練習リポジトリを指している

```bash
git remote -v
git status
gh auth status
gh repo view
```

> [!IMPORTANT]
> 公開リポジトリでは、プロフィールに本名、学籍番号、個人メール、電話番号、住所などを書かないでください。ニックネームで構いません。

## Step 1：Issueを作る

### Web UIで作る

GitHubのIssue template「プロフィール追加」を使います。

例：

```text
プロフィールを追加する：taro
```

### `gh`で作る場合

```bash
gh issue create --title "プロフィールを追加する：taro" --assignee "@me"
```

本文は対話形式で入力します。

Issue番号を控えます。以降は `#12` とします。

どちらから作っても、CLIで同じIssueを確認します。

```bash
gh issue view 12
```

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

> [!TIP]
> Gitのbranch操作を理解した後は、`gh issue develop 12 --checkout --base main --name feature/issue-12-add-profile` のようにIssueとbranch作成をまとめることもできます。

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

ここは`gh`ではなくGitの仕事です。

## Step 6：pushする

```bash
git push -u origin feature/issue-12-add-profile
```

## Step 7：PRを作る

### Web UIで作る

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

### `gh`で作る場合

```bash
gh pr create --base main
```

タイトルと本文を対話形式で入力します。

どちらから作っても、次で同じPRを確認します。

```bash
gh pr status
gh pr view
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

PRの状態やCIをCLIから見る場合：

```bash
gh pr status
gh pr checks
```

## Step 9：merge commitでマージする

基本編ではmerge方式を **Create a merge commit** に固定します。

### Web UI

PR画面で **Create a merge commit** を選びます。

### `gh`

現在branchのPRなら次でも同じmerge方式を選べます。

```bash
gh pr merge --merge
```

マージ後、`Closes #12`によりIssueが閉じたことを確認します。

```bash
gh issue view 12
```

## Step 10：ローカルを片付ける

GitHub上でmergeしただけでは、ローカルGitのmainは自動では更新されません。

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

## Step 11：Web UIと`gh`が同じものを見ていることを確認する

最後に次を実行します。

```bash
gh repo view
gh issue view 12
gh pr status
```

ブラウザでも同じrepo / Issue / PRを開きます。

```text
Web UI  ←→  GitHub service  ←→  gh
                    ↑
                 git push
                    ↑
                 local Git
```

この関係を説明できれば、この教材での`git` / GitHub / `gh`の区別は十分です。

## 完了チェック

- [ ] Issueを作った
- [ ] `gh issue view`で同じIssueを確認した
- [ ] 最新mainからbranchを作った
- [ ] `git diff --staged`を見てからcommitした
- [ ] PRのbase / compareを確認した
- [ ] `gh pr status`または`gh pr view`で同じPRを確認した
- [ ] 同じPRでレビュー修正した
- [ ] merge commitで統合した
- [ ] Web UIのMergeと`gh pr merge --merge`が同じGitHub操作だと説明できる
- [ ] Issueが閉じた
- [ ] local branchを削除した
- [ ] `git log --graph`で履歴を確認した

---

前: [第6章](06_troubleshooting_and_recovery.md)  
次: [第8章 conflict / revert演習](08_conflict_and_revert_practice.md)

公式資料:
- https://cli.github.com/manual/gh_issue_create
- https://cli.github.com/manual/gh_issue_view
- https://cli.github.com/manual/gh_pr_create
- https://cli.github.com/manual/gh_pr_status
- https://cli.github.com/manual/gh_pr_checks
- https://cli.github.com/manual/gh_pr_merge
