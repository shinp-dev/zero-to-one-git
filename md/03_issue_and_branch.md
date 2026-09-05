# 第3章：IssueとBranch — 1つの目的を1つの作業単位にする

## この章のゴール

**IssueをWeb UIまたは`gh`で作り、その目的に対応する作業ブランチを作れる。**

## IssueはWeb UIでも`gh`でも作れる

IssueはGitHub上の同じデータです。入口が違うだけです。

### Web UIから作る

GitHubの **Issues → New issue** を開き、Issue templateがあれば利用します。

### `gh`から作る

```bash
gh issue create --title "プロフィールを追加する：taro" --assignee "@me"
```

本文は対話形式で入力できます。

作成後は一覧と内容をCLIでも確認できます。

```bash
gh issue list
gh issue view 12
```

## Issueに書く3点

```markdown
## 目的
プロフィールを追加し、チームメンバーが担当や学習内容を確認できるようにする。

## やること
- profile_template.mdを複製する
- profiles/<ニックネーム>.mdを作る

## 完了条件
- [ ] 必須項目を記入した
- [ ] profiles/へ保存した
- [ ] PRでレビューした
```

Issueは「作業メモ」ではなく、**何をもって完了とするかを共有する場所**です。

## Web UIと`gh`は同じIssueを見ている

Web UIでIssueを作った場合も、次で見えます。

```bash
gh issue view 12
```

逆に`gh issue create`で作ったIssueも、GitHubのIssues画面に表示されます。

```text
GitHub Web UI ─┐
               ├→ 同じIssue
   gh issue ───┘
```

ここを理解すると、Web操作とCLI操作を別物として暗記しなくて済みます。

## Branchを作る前にmainを最新化する

まずmainへ移動します。

```bash
git switch main
git status
```

未コミット変更がないことを確認してから、GitHubのGitリポジトリ側の状態を取得します。

```bash
git fetch origin
git merge --ff-only origin/main
```

ここでは `fetch` と `merge` を分けています。

```text
git fetch origin
  → remote側の位置を取得する

git merge --ff-only origin/main
  → local mainを、分岐がなければその位置まで進める
```

Issueを作るのは`gh`でもできますが、**local mainの更新はGitの仕事**です。

## 作業ブランチをGitで作る

基本編ではまずGitで作ります。

```bash
git switch -c feature/issue-12-add-profile
```

確認：

```bash
git branch --show-current
git status
```

## `gh`にはIssueとbranchを結ぶショートカットもある

Gitのbranch操作を理解した後なら、GitHub CLIでIssueに紐づくbranchを作成してcheckoutすることもできます。

```bash
gh issue develop 12 \
  --checkout \
  --base main \
  --name feature/issue-12-add-profile
```

これは便利ですが、**基本編の最初は `git switch -c` を使い、branchが何かを理解してから**利用してください。

## この教材の命名規則

```text
種類/issue-番号-短い作業内容
```

例：

```text
feature/issue-12-add-profile
bugfix/issue-21-login-error
docs/issue-8-update-readme
chore/issue-9-update-deps
```

チーム独自ルールがある場合は、そちらを優先します。

## 1つのbranchへ何でも詰め込まない

避けたい例：

```text
feature/issue-12-add-profile
  ├─ プロフィール追加
  ├─ README全面修正
  └─ ライブラリ更新
```

PRを見た人が判断しやすいよう、Issueの目的から外れた変更は別のIssue / branchへ分けます。

## 完了チェック

- [ ] Issueに目的・やること・完了条件を書ける
- [ ] Web UIと`gh issue`が同じIssueを操作していると説明できる
- [ ] `gh issue view`でIssueを確認できる
- [ ] 最新のmainからbranchを作れる
- [ ] branch名からIssueとの対応が分かる
- [ ] `git branch --show-current`で現在地を確認できる
- [ ] `gh issue develop`が便利なショートカットであることを説明できる

---

前: [第2章](02_git_basic_concepts.md)  
次: [第4章 普段のチーム開発フロー](04_team_development_flow.md)

公式資料:
- https://cli.github.com/manual/gh_issue
- https://cli.github.com/manual/gh_issue_create
- https://cli.github.com/manual/gh_issue_develop
