# 第4章：普段のチーム開発フロー

## この章のゴール

**Issue → Branch → Commit → Push → PR → Review → Merge を安全に一周できる。**

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

## 1：最新mainから作業を始める

```bash
git switch main
git status
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

GitHub上で次も確認します。

- base: `main`
- compare: 自分の作業branch
- Files changedに余計なファイルがない

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

## 7：基本編はCreate a merge commitで統合する

この教材の基本編では、GitHubのPR画面で **Create a merge commit** を選びます。

理由：

- branchの履歴がmainへそのまま統合されたことを追いやすい
- `git branch -d`の意味が分かりやすい
- squash / rebaseの履歴変換を初級編へ混ぜない

Squash merge / Rebase mergeは第9章で扱います。

## 8：マージ後に片付ける

```bash
git switch main
git fetch origin
git merge --ff-only origin/main
git branch -d feature/issue-12-add-profile
```

GitHub側の作業branchも不要なら削除します。

## 完了チェック

- [ ] commit前に差分を確認した
- [ ] PRのbase / compareを確認した
- [ ] レビュー修正を同じPRへ追加した
- [ ] Create a merge commitで統合した
- [ ] mainを更新して作業branchを削除した

---

前: [第3章](03_issue_and_branch.md)  
次: [第5章 fetch・merge・conflict](05_sync_and_conflict.md)
