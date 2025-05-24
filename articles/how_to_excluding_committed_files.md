---
title: '任意の過去のコミットを修正する場合'
emoji: '💻'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: [git]
published: false
---

コミットを何回か繰り返した後にコミット対象外のファイルを発見した時の対処方法です。
以下は参考例です。

### 具体例

![コミット一覧](/images/how_to_excluding_committed_files/commit-image.png)

この中で余分なコミットが 2 つ目にあったとします。

![余分コミットファイル](/images/how_to_excluding_committed_files/commit-files.png)

`git` でコミット済みのコードから特定のファイルを除外するには、次の手順を実行します。
具体的には、以下の方法でコミットを修正または変更できます。

### コマンド解説

- `git reset HEAD^ -- <ファイルパス>`: コミットから指定したファイルをインデックスから外します。ただし、ワークツリーの変更内容は保持されます。
- `git commit --amend --no-edit`: 直前のコミットを修正し、新しい内容で上書きします。

### 1. rebase 開始

`git rebase` を使って、過去の特定のコミットを編集します。
今回は 3 つのコミットの二番目が対象です。

```bash
git rebase -i HEAD~3
```

上記コマンドを実行すると下図のようになります。

![git rebase before](/images/how_to_excluding_committed_files/git-rebase-before.png)

### 2. rebase 対象決定

2 つ目のコミットを編集モードにします。

![git rebase after](/images/how_to_excluding_committed_files/git-rebase-after.png)

pick => e(edit)

エディタを esc => wq で閉じます。

![git rebase operation](/images/how_to_excluding_committed_files/git-rebase-operation.png)

### 3. 余分なファイルを除外

```
git reset HEAD^ -- <除外したいファイルのパス>
又は
git reset 'HEAD^' -- <除外したいファイルのパス>
```

:::message alert

zsh の場合、^（キャレット）を使用するとパターン展開が行われてエラーが発生することがあります。
この問題を避けるためには、HEAD^ を引用符で囲む必要があります。
:::

### 4. 変更反映

変更をコミットします。

```bash
git commit --amend --no-edit
```

### 5. rebase 完了

rebase を継続します。

```bash
git rebase --continue
```

実行例です

![git rebase complete](/images/how_to_excluding_committed_files/git-rebase-complete.png)

### 6. 確認

![rebase after log](/images/how_to_excluding_committed_files/rebase-after-log.png)
![rebase after log](/images/how_to_excluding_committed_files/uncommitted-changes.png)

以上で、コミットから不要なファイルを外すことが出来ました。
