# 第6章：IssueからPRまでのハンズオン

## ゴール

`profiles/<名前>.md`を追加し、**Issue → ブランチ → コミット → PR → レビュー → マージ**を完了する。

## 完成までの地図

```text
[GitHub] Issueを作る／選ぶ
      ↓
[PC] mainを最新化 → ブランチ作成
      ↓
[PC] profiles/<名前>.mdを作成 → commit → push
      ↓
[GitHub] PR作成 → レビュー対応 → マージ
      ↓
[PC] mainを更新 → ブランチ削除
```

## 準備チェック

- [ ] GitHubへログインできる
- [ ] このリポジトリをclone済みである
- [ ] ターミナルでリポジトリを開いている
- [ ] `git config user.name`と`git config user.email`に値が出る

> [!NOTE]
> 改行コードの設定はプロジェクトごとに異なります。チーム指定の`.gitattributes`やセットアップ手順を優先してください。

## Step 1：Issueを作る／担当する

GitHubの`Issues`からプロフィール追加用Issueを作成します。用意済みなら自分をAssigneeに設定します。

| 項目 | 内容 |
|---|---|
| タイトル | `プロフィールを追加する：<名前>` |
| 成果物 | `profiles/<名前>.md` |
| 完了条件 | 全項目を記入し、PRでレビュー済み |

Issue番号を控えます。以降の例では`#12`を使います。

## Step 2：ブランチを作る

```bash
git switch main
git pull origin main
git switch -c feature/issue-12-add-profile
```

✅ `git status`の先頭に作業ブランチ名が表示されれば完了です。

## Step 3：プロフィールを作る

1. [`profile_template.md`](../profile_template.md)をコピーする
2. `profiles/<名前>.md`として保存する
3. 角括弧のプレースホルダーをすべて書き換える

例：`profiles/taro.md`

## Step 4：確認してコミットする

```bash
git status
git add profiles/taro.md
git diff --staged
git commit -m "feat: taroのプロフィールを追加"
```

✅ `git diff --staged`で、プロフィール以外の変更が含まれていないことを確認します。

## Step 5：GitHubへpushする

```bash
git push -u origin feature/issue-12-add-profile
```

✅ GitHubに作業ブランチが表示されれば完了です。

## Step 6：PRを作る

GitHubの`Compare & pull request`を開きます。

```markdown
## 変更内容
- taroのプロフィールを追加

## 確認
- [x] テンプレートの全項目を記入した
- [x] profiles/に保存した

Closes #12
```

✅ 変更ファイルが1件で、baseが`main`、compareが作業ブランチになっていることを確認します。

## Step 7：レビューへ対応する

指摘がなければ承認へ進みます。指摘があれば同じブランチで修正します。

```bash
git add profiles/taro.md
git commit -m "fix: プロフィールの記載漏れを修正"
git push
```

✅ 新しいPRは作りません。現在のPRへコミットが追加されます。

## Step 8：マージして片付ける

PRをマージし、GitHub上の作業ブランチを削除します。その後、PC側を更新します。

```bash
git switch main
git pull origin main
git branch -d feature/issue-12-add-profile
```

## 完了チェック

- [ ] PRがマージされた
- [ ] `Closes #12`によりIssueが閉じた
- [ ] `profiles/<名前>.md`が`main`にある
- [ ] ローカルの作業ブランチを削除した

## GitHubを使えない場合：ローカル練習版

Step 4の後、次だけを実行するとマージを疑似体験できます。

```bash
git switch main
git merge feature/issue-12-add-profile
git branch -d feature/issue-12-add-profile
```

この方法ではIssue、PR、レビューは体験できません。可能になったら本編も実施してください。

---

* [前へ：第5章](05_troubleshooting_and_recovery.md)
* [総合目次](git_team_development_guide.md)
