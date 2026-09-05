# 第6章：トラブルシューティングと復旧

## この章のゴール

**「何を戻したいか」と「共有済みか」を見て、安全な操作を選べる。**

## 最初の原則

```text
分からない
  ↓
追加操作を止める
  ↓
git status
  ↓
git log / git diffで状況を見る
  ↓
共有済みか確認する
```

## 逆引き表

| 状況 | 基本の操作 | 変更内容 |
|---|---|---|
| 未commitの編集を捨てたい | `git restore <file>` | 編集が消える |
| addだけ取り消したい | `git restore --staged <file>` | 編集は残る |
| 未pushの直前commitをやり直したい | `git reset HEAD~1` | commitだけ戻し、編集は残る |
| 共有済みcommitを打ち消したい | `git revert <commit>` | 取り消し用の新commitを作る |
| merge途中を中止したい | `git merge --abort` | merge開始前へ戻す |
| commit文だけ直したい（未push） | `git commit --amend` | 直前commitを書き換える |

## 最重要：resetとrevertを分ける

### まだpushしていない

直前のcommitを取り消して編集状態へ戻す：

```bash
git reset HEAD~1
```

これはbranch / HEADの位置を動かします。

### すでにpushした・他人と共有した

```bash
git revert <commit-id>
```

`revert`は元の履歴を消さず、「その変更を打ち消す新しいcommit」を作ります。

```text
A ← B ← C ← Revert C
```

共有履歴ではこちらを基本にします。

## `git commit --amend`も共有後は注意

未pushなら、直前commitのメッセージや内容を整えるのに便利です。

```bash
git add <file>
git commit --amend
```

push済みcommitへamendするとcommit IDが変わり、通常pushできなくなります。共有後は個人判断で履歴を書き換えません。

## `reset --hard`とforce push

次は強い操作です。

```bash
git reset --hard <commit>
git push --force-with-lease
```

- 未commit変更を失うことがある
- 共有履歴を書き換えることがある
- `main`や共有branchでは個人判断で実行しない

この教材の基本編では、復旧の第一候補にしません。

## 秘密情報をpushした

最優先は履歴編集ではありません。

```text
1. 漏洩した鍵・トークン・パスワードを無効化 / 再発行
2. チーム責任者へ連絡
3. 公開範囲と影響を確認
4. 必要なら管理者手順で履歴から削除
5. .gitignoreやSecret管理を修正
```

ファイルを削除するcommitだけでは、過去の履歴から消えません。

## どうしてもcommitが見つからない

Gitは最近のHEAD移動を `reflog` に残している場合があります。

```bash
git reflog
```

ただし復旧対象を誤ると混乱しやすいため、初心者は結果を保存して相談してから進めます。

## 完了チェック

- [ ] `restore --staged`と`restore`の違いを説明できる
- [ ] 未pushならreset、共有済みならrevertという原則を説明できる
- [ ] amend後のcommit IDが変わることを理解している
- [ ] 秘密情報漏洩時に最初に鍵を無効化できる

---

前: [第5章](05_sync_and_conflict.md)  
次: [第7章 PRハンズオン](07_hands_on_practice.md)

公式資料:
- https://git-scm.com/docs/git-revert
- https://git-scm.com/docs/git-reset
