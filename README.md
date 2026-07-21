# 🎓 Git/GitHubチーム作業の基本

GitHubを使ったチーム作業へ入る前に、メンバー全員で共有しておきたい**基本的な前提知識**をまとめた日本語ガイドです。

Gitの基本概念、Issue、ブランチ、コミット、PR、レビュー、マージ、トラブル対応を、「何のために行う操作か」から図・表・チェックリストで学びます。最後に一連の流れをハンズオンで確認できます。

## まず見る全体像

```text
Issueを選ぶ → ブランチを作る → 編集・コミット → push → PR → レビュー → マージ
```

## こんな人におすすめ

- Gitを初めて使う人
- 個人開発からチーム開発へ進みたい人
- GitHubを使うプロジェクトへ参加する前の人
- チーム内でGit/GitHubの認識を揃えたい人
- Issue・ブランチ・PRのつながりを練習したい人

| 項目 | 目安 |
|---|---|
| 前提知識 | ファイル作成とターミナルの基本操作 |
| 必要なもの | Git、GitHubアカウント、テキストエディタ |
| 所要時間 | 読解30〜45分＋ハンズオン30〜60分 |

## 最短ルート

| 目的 | 開くページ |
|---|---|
| まず全体を知る | [総合ガイド](md/git_team_development_guide.md) |
| すぐ手を動かす | [第6章：ハンズオン](md/06_hands_on_practice.md) |
| エラーから戻したい | [第5章：トラブル対応](md/05_troubleshooting_and_recovery.md) |

## 学習コンテンツ

| 章 | テーマ | 読了後にできること |
|---|---|---|
| [1](md/01_why_git_and_github.md) | Git/GitHubを使う理由 | ブランチやPRの目的を説明できる |
| [2](md/02_git_basic_concepts.md) | 基本概念とコマンド | 変更をコミットして共有できる |
| [3](md/03_branch_naming_rules.md) | ブランチ名 | Issueに対応した名前を付けられる |
| [4](md/04_team_development_flow.md) | チーム開発フロー | Issueからマージまで進められる |
| [5](md/05_troubleshooting_and_recovery.md) | 復旧方法 | 状況に合う安全な戻し方を選べる |
| [6](md/06_hands_on_practice.md) | 実践 | 自己紹介をPRで追加できる |

## ハンズオンの成果物

- Issue：作業の目的と完了条件
- ブランチ：`feature/issue-<番号>-add-profile`
- プロフィール：`profiles/<名前>.md`
- PR：説明文に `Closes #<Issue番号>` を記載

## 始め方

1. このリポジトリをForkする
2. Forkしたリポジトリをcloneする
3. [第6章：ハンズオン](md/06_hands_on_practice.md)を開く
4. プロフィール追加用Issueを作成して進める

```bash
git clone https://github.com/<GitHubユーザー名>/zero-to-one-git.git
cd zero-to-one-git
```

> [!TIP]
> GitHubを使えない場合は、第6章の「ローカル練習版」だけでもGitの基本操作を試せます。

## ライセンス

[MIT License](LICENSE)
