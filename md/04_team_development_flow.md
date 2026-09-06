# 第4章：普段のチーム開発フロー

## この章のゴール

**Issue → Branch → Commit → Push → PR → Review → Merge を安全に一周し、GitHub上の操作をWeb UIと`gh`の両方から確認できる。**

## 全体像

```text
Issue
 ↓
最新mainからbranch作成
 ↓
編集
 ↓
status / diff
 ↓
add / diff --staged
 ↓
commit
 ↓
push
 ↓
Pull Request
 ↓
Review / 修正
 ↓
Create a merge commit
 ↓
main更新 / branch削除
```

## Gitと`gh`の境界

この章では、まず次のように分けます。

| 操作 | 主に使うもの |
|---|---|
| 現在branch・差分・stagingを見る | Git |
| commitする | Git |
| remoteへpush / fetchする | Git |
| Issue / PRを作る・見る | GitHub Web UI または `gh` |
| PRのCI状態を見る | GitHub Web UI または `gh pr checks` |
| PRをGitHub上でmergeする | GitHub Web UI または `gh pr merge` |

`gh`はGitHub側の操作をCLIに持ってくる道具で、`git add`や`git commit`の代わりではありません。

## 1：最新mainから作業を始める

最初の`git status`で未commit変更がある場合は、現在の作業をcommitするか退避方針を決めてから、branchを切り替えます。

```bash
git status
git switch main
git fetch origin
git merge --ff-only origin/main
git switch -c feature/issue-12-add-profile
```

## 2：編集したら差分を見る

```bash
git status
git diff
```

「何を変えたか」を確認せずに全部addしないことを基本にします。

新規ファイルは未追跡の間、通常の`git diff`には出ません。`git status`で対象を確認し、ファイルを開くか、次の手順でaddしてから中身を確認します。

## 3：次のcommitに入れる変更を選ぶ

```bash
git add profiles/taro.md
git diff --staged
```

意図した変更だけならcommitします。

```bash
git commit -m "feat: taroのプロフィールを追加"
```

## 4：GitHubへpushする

初回：

```bash
git push -u origin feature/issue-12-add-profile
```

2回目以降：

```bash
git push
```

ここまではGitの仕事です。

## 5：PRを作る

PRには最低限、次を書きます。

```markdown
## 変更内容
- taroのプロフィールを追加

## 確認内容
- [x] テンプレートの必須項目を記入した
- [x] 意図しないファイルを含んでいない

Closes #12
```

### Web UIから作る

GitHubのPull requests画面から作り、次を確認します。

- base: `main`
- compare: 自分の作業branch
- Files changedに余計なファイルがない

### `gh`から作る

現在のbranchをpush済みなら、次でも作れます。

```bash
gh pr create --base main
```

タイトルと本文を対話形式で入力します。

作成後はCLIからも確認できます。

```bash
gh pr status
gh pr view
```

Web UIで作ったPRも`gh pr view`で見え、`gh pr create`で作ったPRもWeb UIに表示されます。

## 6：レビュー指摘は同じbranchで直す

```bash
git status
# ファイルを修正
git add profiles/taro.md
git diff --staged
git commit -m "fix: プロフィールの記載漏れを修正"
git push
```

開いているPRへ自動的に反映されます。指摘のたびに新しいPRを作る必要はありません。

GitHub CLIからPRの状態を確認するなら：

```bash
gh pr status
gh pr checks
```

`gh pr checks`はPRに紐づくCIの状態を確認します。Actionsが無い教材repoでは何も表示されない場合があります。

## merge前に確認すること

AIがcommitまで済ませた場合は、PRのFiles changedまたは`gh pr diff`で提出する変更全体を確認します。AIの要約だけでは、変更漏れや不要な削除を見落とすことがあります。

- Issueの完了条件と実際の変更が一致しているか
- 変更に合った検証結果があり、未実施の確認と区別されているか
- レビュー後に追加されたcommitも確認したか

CIがないことはテスト成功を意味しません。この教材のプロフィール変更なら、内容・公開情報・Markdown表示を確認します。アプリの変更なら、該当機能の正常系や失敗時の動作も確認します。

## 7：基本編はCreate a merge commitで統合する

この教材の基本編では、merge方式を **merge commit** に固定します。

### Web UI

PR画面で **Create a merge commit** を選びます。

### `gh`

現在branchのPRをmergeする場合：

```bash
gh pr merge --merge
```

どちらもGitHub上の同じPRをmergeしています。

理由：

- branchの履歴がmainへそのまま統合されたことを追いやすい
- `git branch -d`の意味が分かりやすい
- squash / rebaseの履歴変換を初級編へ混ぜない

Squash merge / Rebase mergeは第9章で扱います。

## 8：マージ後に片付ける

GitHub上でmergeした後、ローカルGitを更新します。

```bash
git switch main
git fetch origin
git merge --ff-only origin/main
git branch -d feature/issue-12-add-profile
```

GitHub側の作業branchも不要なら削除します。

ここも「GitHub上のmerge」と「ローカルGitの更新」は別操作だと意識してください。

## Web UIと`gh`はどちらを使う？

```text
初めて操作する
→ Web UIで画面上の対象を確認しやすい

同じ操作を繰り返す / ターミナル中心で作業する
→ ghが速い
```

どちらか一方だけが正解ではありません。**同じGitHub上のIssue / PRを別の入口から操作できる**と理解できればOKです。

## 完了チェック

- [ ] commit前に差分を確認した
- [ ] PRのbase / compareを確認した
- [ ] `gh pr status`または`gh pr view`で同じPRを確認した
- [ ] レビュー修正を同じPRへ追加した
- [ ] `gh pr checks`が何を見るコマンドか説明できる
- [ ] merge commitで統合した
- [ ] Web UIのMergeボタンと`gh pr merge --merge`が同じGitHub上のPRを操作すると説明できる
- [ ] mainを更新して作業branchを削除した

---

前: [第3章](03_issue_and_branch.md)  
次: [第5章 fetch・merge・conflict](05_sync_and_conflict.md)

公式資料:
- https://cli.github.com/manual/gh_pr
- https://cli.github.com/manual/gh_pr_create
- https://cli.github.com/manual/gh_pr_status
- https://cli.github.com/manual/gh_pr_checks
- https://cli.github.com/manual/gh_pr_merge
