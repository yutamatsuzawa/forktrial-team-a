# WS3 : リポジトリのフォーク＆クローン演習

この演習では、このリポジトリ (ict4e-hara/forktrial) をあなたのPCにフォーク＆クローンして、基本的な操作（ブランチ作成、コミット、プッシュ、Pull Request 作成）を行う手順を学びます。

---

## 前提
- Git がインストールされていること（バージョン確認: `git --version`）
- GitHub アカウントを持っていること
- SourceTreeを使う場合、GitHubアカウントがSourceTreeに登録済みであること
- SSH の設定を使う場合は SSH 鍵を GitHub に登録していること

---

## 1-1. リポジトリをフォーク
研修で配布リポジトリを自分のアカウントにコピーするため、次のリポジトリをブラウザで開き、右上の "Fork" ボタンを押して自分の GitHub アカウントへフォークします。

- https://github.com/ict4e-hara/forktrial


（直接クローンしても演習はできますが、PR を送る練習をするためにフォークしてください）

---

## 1-2. クローン（Sourcetree）　※推奨
Sourcetree を使う場合の手順:

1. Sourcetree の リポジトリブラウザ を表示
2. 「リモート」ボタンを押して、あなたの GitHub アカウント配下に、Forkした forktrial リポジトリが表示
3. 隣にある「クローン」リンクを押して、必要情報を入力


## 1-2 (a). クローン（HTTPS + コマンド）
HTTPS を使う場合の手順:

1. フォークしたリポジトリページで "Code" ボタンを押し、"HTTPS" の URL をコピー。
2. ターミナルでクローンするディレクトリに移動して次を実行:

```bash
# 例: HTTPS を使ってクローン
git clone https://github.com/<あなたのユーザ名>/forktrial.git
cd forktrial
```

※または元リポジトリを直接クローンするには  https://github.com/ict4e-hara/forktrial.git を使用します。

---

## 1-2 (b). クローン（SSH + コマンド）
SSH を使う場合の手順:

1. GitHub に SSH 鍵を登録済みであることを確認します（ https://github.com/settings/keys ）。
2. リポジトリの "Code" で SSH の URL をコピーし、次を実行:

```bash
# 例: SSH を使ってクローン
git clone git@github.com:<あなたのユーザ名>/forktrial.git
cd forktrial
```

※または元リポジトリを直接クローンするには git@github.com:ict4e-hara/forktrial.git を使用します。

---

## 1-2. リモートの確認
クローン後、どのリモートが設定されているか確認します:

### GUI手順

```bash
forktraial の ウィンドウを開く
設定 > 「リモート」タブを確認
```

### コマンド手順

```bash
git remote -v
```

出力例（フォークをクローンした場合）:

```
origin  https://github.com/<あなたのユーザ名>/forktrial.git (fetch)
origin  https://github.com/<あなたのユーザ名>/forktrial.git (push)
```

元リポジトリ（upstream）を追加しておくと便利です（main を同期するため）:

```bash
git remote add upstream https://github.com/ict4e-hara/forktrial.git
# 確認
git remote -v
```

---

## 1-3. 作業を行いプルリクエストを送る

### GUI手順

1. Sourcetree で ブランチ `feature/<あなたの名前>-intro` を作る
2. ファイルを作成/編集 `exercises/<あなたの名前>-intro.md` に自己紹介を書く
3. 変更をステージしてコミット
4. リモートへプッシュ
5. GitHub 上で Pull Request を作成して、オリジナルのリポジトリにPRを投げる


### コマンド手順

1. ブランチを作る

```bash
git checkout -b feature/<あなたの名前>-intro
```

2. ファイルを作成/編集（例: exercises/<あなたの名前>-intro.md に自己紹介を書く）

3. 変更をステージしてコミット

```bash
git add exercises/<あなたの名前>-intro.md
git commit -m "Add: your-name exercise file"
```

4. リモートへプッシュ

```bash
git push origin feature/<あなたの名前>-intro
```

5. GitHub 上で Pull Request を作成して、オリジナルのリポジトリにPRを投げる


---

## 1-4. mainブランチの更新

Fork元リポジトリのmainブランチ更新を、自身のリポジトリ（Fork先）にも反映しましょう。

### GUI手順

1. フォークしたリポジトリページ（自身のリポジトリ）の mainブランチ で "Sync fork" ボタンを押す
2. ブランチの状態が表示され "out-of-date" の場合には "Update branch" ボタンを押して最新化する
3. Sourcetree で "フェッチ” ボタンを押して、リモートの最新状態を取り込み
4. mainブランチを開き "プル" を押して、最新化する


---

## a. 演習タスク まとめ
1-1. このリポジトリをフォーク
1-2. クローンする
1-3. `feature/<あなたの名前>-intro` ブランチを作成
3. `exercises/<あなたの名前>-intro.md` を作成し、名前・所属・今日の学びなどを記載
4. コミットしてプッシュ、PR を作成してレビュー／マージを体験


---

## b. 確認コマンド・デバッグ
- 現在のブランチ: `git branch --show-current`
- 変更の状態: `git status`
- ログ確認: `git log --oneline --graph --decorate -n 20`
- リモートの取得: `git fetch upstream`
- main を最新にする（マージ）:

```bash
git checkout main
git fetch upstream
git merge upstream/main
```


---

## c. よくあるトラブルと対処
- 認証エラー（HTTPS）: パスワード入力が求められる場合は PAT（Personal Access Token）の使用を検討してください。GitHub はパスワード認証を廃止しています。
- SSH が使えない/Permission denied: SSH 鍵が登録されているか確認し、`ssh -T git@github.com` で接続テストを行ってください。
- push が拒否された: リモートの main に自分のローカルが追いついていない可能性があります。`git pull --rebase` や upstream から取り込んで解決してください。


---

## 1-9. リモートリポジトリを複数設定する

Fork元リポジトリを、Sourcetreeに設定して mainブランチの最新化を容易にしましょう。

### GUI手順

1. Sourcetree で "設定” ボタンを押して、「リモート」タブを開く。現在は origin のみが登録されている。
2. リモートリポジトリのパス の 「追加」ボタンを押す
3. 表示されるダイアログボックスに、次の情報を記載する
   - リモートの名前： upstream
   - URL/パス : https://github.com/ict4e-hara/forktrial.git
   - その他の情報は、自動で入力される
5. Sourcetree の 履歴View で upstrem/main リモート追跡ブランチ が表示されるようになる
6. また、mainブランチを開き "プル" を押すと、「プルする元のリポジトリ」 として 「upstream」 が選択出来るようになる


---

## 参考
- Git 入門: https://git-scm.com/book/ja/v2
- GitHub SSH 鍵の設定: https://docs.github.com/ja/authentication/connecting-to-github-with-ssh

---

このファイルを使って演習を進めてください。問題が出たら `git status` や `git log` の出力を教えてください。
