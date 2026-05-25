# 第6章：手を動かして学ぶ実践ハンズオン

これまで学んだ一連の流れを、手元のPCで実際に動かして体験してみましょう。
練習用の自己紹介テンプレートを利用して、**「作業用ブランチの作成から、ファイルを編集し、mainブランチに合流させて後片付けするまで」**のワークフローを疑似体験します。

---

## 6.1 【準備】Gitの初期設定と環境確認

コマンドを動かす前に、PCの初期設定と設定状況を確認します。

### 1. ターミナル（Git Bash推奨）の起動とフォルダ移動
Gitのコマンドを実行するため、ターミナル（Windowsは Git Bash または PowerShell）を起動し、このプロジェクトのリポジトリ（フォルダ）に移動します。

```bash
# このリポジトリの場所に移動する
cd d:/zerotoone-git
```

### 2. ユーザー設定の確認と設定
Gitで履歴を記録する際、「誰がコミットしたか」を識別するための名前とメールアドレスを設定します。

```bash
# 現在の設定状況を確認する
git config user.name
git config user.email
```
* **もし何も表示されない（未設定）場合**は、以下のコマンドで設定します。
  ```bash
  git config --global user.name "あなたの名前（アルファベット推奨）"
  git config --global user.email "your-email@example.com"
  ```

### 3. Windows環境の改行コード設定（Windowsユーザーは必須）
WindowsとMac/Linuxの間で改行コードの違いによる不要な差分が出るのを防ぐため、以下の自動変換設定を有効にします。

```bash
git config --global core.autocrlf true
```

---

## 6.2 【実践】ハンズオンスタート

今回は、GitHubを使わずにローカルPC内だけで一人二役（開発者 ＆ マージャー）を行い、一連のGit操作の流れを体験します。

### Step 1: タスク（やること）の確認
* **課題（イシュー）**: `練習リポジトリに自分の自己紹介シートを追加する`
* **作業するフォルダ**: `d:/zerotoone-git`
* **作成する作業ブランチ名**: `feature/issue-1-introduce-myself`

---

### Step 2: 最新の main ブランチから新しいブランチを作る
安全な作業スペースを確保するため、本番用ブランチから自分専用のブランチ（部屋）を分岐させます。

```bash
# 1. 本番用の main ブランチにいることを確認する
git switch main

# 2. 最新のリモート状態を取り込む（今回はローカル練習のためそのまま進みます）
# git pull origin main

# 3. 新しい作業用ブランチを作成して、同時に切り替える
git switch -c feature/issue-1-introduce-myself
```

切り替えに成功すると、ターミナルに `Switched to a new branch 'feature/issue-1-introduce-myself'` と表示されます。

---

### Step 3: ファイルを作成・編集する
エディタ（VS Codeなど）を使い、新しいファイルを作成します。

1. このプロジェクトにある [profile_template.md](../profile_template.md) を開きます。
2. ファイルの内容をすべてコピーします。
3. 同じフォルダ（`d:/zerotoone-git`）の直下に、新しく `profile_yourname.md` （例: `profile_taro.md` など、ご自身の名前）というファイルを新規作成し、コピーした内容を貼り付けます。
4. ファイル内の `[ここに名前を書いてください]` などのプレースホルダーをご自身の情報に書き換えて保存します。

---

### Step 4: 変更をステージングエリアに追加し、コミットする
作成したファイルをセーブポイント（コミット）に記録します。

```bash
# 1. 現在の状態を確認する
git status
# 新しく作ったファイル（例: profile_taro.md）が「Untracked files」として赤文字で表示されます。

# 2. 作成したファイルをステージングエリア（コミット待ち台車）に載せる
git add profile_taro.md

# 3. 再度状態を確認する
git status
# ファイル名が緑文字（Changes to be committed）に変わり、コミット準備完了になります。

# 4. コミットを実行する
git commit -m "feat: taroの自己紹介シートを追加"
```

これで、あなたのローカルPCのデータベースに変更履歴がセーブされました。

---

### Step 5: ローカルでのマージ（合流）体験
通常であればここで `git push origin <ブランチ名>` でGitHubにアップしてプルリクエストを作成しますが、今回はローカル環境だけでマージの動きをシミュレートします。

```bash
# 1. 本番用の main ブランチに戻る
git switch main

# 2. あなたが作った作業ブランチの変更を main に合流させる（マージ）
git merge feature/issue-1-introduce-myself
```

マージを実行すると、ターミナルに `Fast-forward` や更新情報が表示されます。
エディタのファイル一覧を見てみましょう。`main` ブランチにいる状態でも、先ほど作成した `profile_yourname.md` がしっかりとフォルダ内に存在しているはずです！

---

### Step 6: 後片付け（ブランチの削除）
無事にマージ（統合）が完了したら、役割を終えたブランチは削除して整理整頓します。

```bash
# 不要になった作業ブランチをローカルから削除する
git branch -d feature/issue-1-introduce-myself
```
* ※間違えてマージしていないブランチを削除しようとするとGitがエラー警告を出してくれます。 `-d` オプションは安全に削除するためのものです。

これで、ブランチの作成からマージ、後片付けまでの基本的なGitワークフローの体験は完了です！

---

* [前へ（第5章：トラブルシューティングとリカバリー方法）](05_troubleshooting_and_recovery.md)
* [総合目次に戻る](git_team_development_guide.md)
