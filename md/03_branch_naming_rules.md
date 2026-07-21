# 第3章：ブランチの命名規則

## この章のゴール

**ブランチ名だけで、作業の種類と対応Issueを伝えられる。**

## 基本形

```text
種類 / issue-番号 - 作業内容
  │       │          └─ 短い英単語
  │       └──────────── Issueとの対応
  └──────────────────── 作業カテゴリ
```

例：`feature/issue-12-user-login`

## 種類を選ぶ

| 種類 | 使う場面 | 例 |
|---|---|---|
| `feature/` | 機能を追加する | `feature/issue-12-user-login` |
| `bugfix/` | 通常の不具合を直す | `bugfix/issue-45-payment-error` |
| `hotfix/` | 緊急修正を行う | `hotfix/issue-51-login-outage` |
| `docs/` | 文書を直す | `docs/issue-8-update-readme` |
| `chore/` | 設定や保守作業を行う | `chore/issue-9-update-deps` |

## 命名チェック

- [ ] 小文字で統一した
- [ ] 単語をハイフンで区切った
- [ ] Issue番号を含めた
- [ ] 作業内容を短い英単語で表した
- [ ] チーム固有の規則があれば、そちらを優先した

| 分かりやすい | 分かりにくい | 理由 |
|---|---|---|
| `feature/issue-12-user-login` | `my-work` | 目的が分からない |
| `bugfix/issue-45-payment-error` | `fix` | 対象が分からない |
| `docs/issue-8-update-readme` | `README直す` | 環境によって入力・参照しづらい |

> [!NOTE]
> Gitのブランチ名には大文字や日本語を使用できます。ただし、表記揺れや入力ミスを避けるため、この教材では小文字の英数字、ハイフン、スラッシュに統一します。

---

* [前へ：第2章](02_git_basic_concepts.md)
* [総合目次](git_team_development_guide.md)
* [次へ：第4章](04_team_development_flow.md)
