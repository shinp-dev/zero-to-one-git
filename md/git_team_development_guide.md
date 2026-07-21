# Git/GitHubチーム開発ガイド

## 7秒で分かる全体像

```text
Issue → Branch → Commit → Push → Pull Request → Review → Merge
 何を     分離       記録      共有       確認依頼        合意      統合
```

## 目的別ナビゲーション

| 今したいこと | 読む場所 |
|---|---|
| なぜ必要か知りたい | [第1章](01_why_git_and_github.md) |
| 基本コマンドを確認したい | [第2章](02_git_basic_concepts.md) |
| ブランチ名を決めたい | [第3章](03_branch_naming_rules.md) |
| 通常の開発手順を確認したい | [第4章](04_team_development_flow.md) |
| 失敗から戻したい | [第5章](05_troubleshooting_and_recovery.md) |
| 一連の流れを練習したい | [第6章](06_hands_on_practice.md) |

## 作業中のクイックガイド

| やること | コマンド／操作 |
|---|---|
| `main`を最新にする | `git switch main` → `git pull origin main` |
| ブランチを作る | `git switch -c feature/issue-12-add-profile` |
| 状態を確認する | `git status` |
| 変更を記録する | `git add <ファイル>` → `git commit -m "説明"` |
| GitHubへ送る | `git push -u origin <ブランチ>` |
| PRとIssueを結ぶ | PR本文に`Closes #12` |
| マージ後に片付ける | `git switch main` → `git pull` → `git branch -d <ブランチ>` |

## 困ったとき

```text
止まる → git status → メッセージを読む → 第5章の逆引き表 → 必要なら相談
```

> [!WARNING]
> `reset --hard`やforce pushは、変更や共有履歴を失う可能性があります。対象と影響が分からない状態では実行しません。

## 学習の進め方

- 初めての人：第1章から順番に進む
- 操作しながら覚える人：第6章を開き、必要な章を参照する
- 作業中の人：上のクイックガイドと第5章を使う

---

* [リポジトリのREADME](../README.md)
* [ハンズオンを始める](06_hands_on_practice.md)
