# 第3章：IssueとBranch — 1つの目的を1つの作業単位にする

## この章のゴール

**Issueの目的と対応する作業ブランチを作れる。**

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

## Branchを作る前にmainを最新化する

まずmainへ移動します。

```bash
git switch main
git status
```

未コミット変更がないことを確認してから、GitHubの状態を取得します。

```bash
git fetch origin
git merge --ff-only origin/main
```

ここでは `fetch` と `merge` を分けています。

```text
git fetch origin
  → GitHub側の位置を取得する

git merge --ff-only origin/main
  → local mainを、分岐がなければその位置まで進める
```

## 作業ブランチを作る

```bash
git switch -c feature/issue-12-add-profile
```

確認：

```bash
git branch --show-current
git status
```

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
- [ ] 最新のmainからbranchを作れる
- [ ] branch名からIssueとの対応が分かる
- [ ] `git branch --show-current`で現在地を確認できる

---

前: [第2章](02_git_basic_concepts.md)  
次: [第4章 普段のチーム開発フロー](04_team_development_flow.md)
