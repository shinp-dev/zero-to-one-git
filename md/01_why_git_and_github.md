# 第1章：なぜGit/GitHubを使うのか

## この章のゴール

**Git / GitHub / `gh` の役割と、Issue・Branch・Commit・PRが解決する問題を説明できる。**

## Git / GitHub / `gh` は別のもの

| 名前 | 主な役割 | ひとことで |
|---|---|---|
| Git | PC内で変更履歴、branch、commit、remote同期を扱う | 履歴を作る仕組み |
| GitHub | Gitの履歴を共有し、IssueやPRで協働する | チームの作業場所 |
| `gh` | GitHubをターミナルから操作する公式CLI | GitHub Web UIのCLI版 |

GitはGitHubがなくても使えます。GitHubはGitを使った共同作業をしやすくするサービスです。`gh`は、そのGitHubサービスをブラウザを開かずに操作するための道具です。

```text
ローカルPC
├─ git status / add / commit / branch / merge
│        ↓ push / fetch
└──────── Git remote

GitHub
├─ Repository
├─ Issue
├─ Pull Request
├─ Review
└─ Actions
   ↑            ↑
 Web UI       gh CLI
```

## どこが重なって、どこが重ならない？

同じGitHub操作へ複数の入口がある場合があります。

```text
GitHubのIssue画面  ←→ gh issue
GitHubのPR画面     ←→ gh pr
GitHubのrepo画面   ←→ gh repo
```

一方、次はGit本体の仕事です。

```text
git diff
git add
git commit
git branch
git fetch
git merge
```

`gh`を覚えても、Gitの状態管理を理解しなくてよいわけではありません。

> [!NOTE]
> `gh repo clone`のようにGitの操作を便利に呼び出す機能もあります。まず「何をしているか」をGit側で理解し、その後に`gh`のショートカットを使う方針にします。

## チーム開発で困ること

| 困ること | 仕組み |
|---|---|
| 何のための作業か分からない | Issue |
| 作業中の変更をmainから分離したい | Branch |
| 変更を意味のある単位で残したい | Commit |
| 他人へ確認してもらいたい | Pull Request |
| 変更を統合したい | Merge |

```text
Issue（目的）
   ↓
Branch（作業を分離）
   ↓
Commit（変更を記録）
   ↓
Pull Request（差分と判断材料を共有）
   ↓
Review（確認）
   ↓
Merge（mainへ統合）
```

## `main`を直接編集しない理由

`main`は「チームが統合済みの成果として参照する中心ブランチ」です。

作業ブランチを使えば、開発途中の変更をmainから分けたまま、次を確認できます。

- Issueの目的と変更が一致しているか
- 意図しないファイルを触っていないか
- テストや動作確認が済んでいるか
- レビューで問題がないか

> [!IMPORTANT]
> **作業はbranch、確認はPR、統合先はmain。** まずこの流れを固定します。

## Gitで残したいのは「保存履歴」だけではない

良い履歴は、未来の自分や他の人が次を判断する材料になります。

```text
何を変えた？
なぜ変えた？
どのIssueのため？
どこまで確認した？
```

Gitを使う目的は履歴を綺麗に見せることではありません。**変更の意図と復旧可能性を残すこと**です。

## 完了チェック

- [ ] GitとGitHubの違いを説明できる
- [ ] `gh`が何を操作する道具か説明できる
- [ ] `git add` / `git commit`を`gh`が置き換えるわけではないと説明できる
- [ ] Issue / Branch / Commit / PR / Mergeの目的を1文ずつ説明できる
- [ ] mainへ直接作業しない理由を説明できる

---

前: [第0章](00_setup_and_auth.md)  
次: [第2章 Gitの地図](02_git_basic_concepts.md)
