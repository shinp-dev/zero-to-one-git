# 教材リポジトリの推奨GitHub設定

このファイルは教材管理者向けです。教材本文とGitHub上の実際の運用を揃えるため、次の設定を推奨します。

## 1. Template Repository

**Settings → General → Template repository** をONにします。

基本編をForkではなく、自分専用repoを生成して行えるようになります。

公式資料: https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository

## 2. Merge button

基本教材では **Create a merge commit** を使用します。

授業で選択ミスを減らしたい場合は、教材運用中だけ次のように統一します。

- Allow merge commits: ON
- Allow squash merging: OFF
- Allow rebase merging: OFF

実務向け教材として3方式を見せたい場合は全てONでも構いません。その場合も基本編ではCreate a merge commitを選ぶよう案内します。

## 3. Automatically delete head branches

ON推奨です。

PRマージ後のGitHub側作業branchを自動削除し、不要branchを残しにくくします。

## 4. mainへの直接pushを防ぐ

共有教材repo自体を複数人で編集する場合はRuleset / Branch protectionで `main` へのPull Requestを要求することを推奨します。

最低限の考え方：

```text
mainへ直接pushしない
  ↓
branchで変更
  ↓
PRで確認
  ↓
merge
```

学生がTemplateから作った個人練習repoでは、保護設定まで同じにする必要はありません。

## 5. Issues

ハンズオンでIssueを使うためONにします。

## 6. 教材更新時の確認

- [ ] READMEの学習順序と実ファイルが一致している
- [ ] Issue / PR templateが表示される
- [ ] 基本編がFork前提になっていない
- [ ] `git pull`を「単なる取得」と説明していない
- [ ] reset / revertの共有状態による使い分けがある
- [ ] conflict演習が実行可能
- [ ] 公開プロフィールの個人情報注意がある
