---
title: '削除した git stash の復元手順'
emoji: '⏮'
type: 'tech'
topics: ['github', 'tech']
published: false
---

## 削除した git stash の復元手順

Github の stash をうっかり削除してしまった時の復元手順をまとめてみました。

### 削除された stash の候補となる SHA1 ハッシュの捜索

```sh
$ git fsck --no-reflog | awk '/dangling commit/ {print $3}'
```

### 見つかった SHA1 ハッシュの内容を確認

```sh
$ git log --oneline --graph --decorate $(git fsck --no-reflog | awk '/dangling commit/ {print $3}') | grep -i "stash"
```

削除された stash の候補を表示し、"stash" という単語を含むものをフィルタリングします。
メッセージ付きの stash は通常、このリストに表示されます。

### 目的の stash の内容を詳しく確認

```sh
$ git show [見つかったSHA1ハッシュ]
```

### 復元したい stash をコマンドで復元

```sh
$ git stash apply [見つかったSHA1ハッシュ]
```

この方法で、メッセージ付きで削除してしまった stash を効率的に探し出し、復元することができます。

:::message alert
注意点
:::

- この方法は、git の内部データベースを直接探索するため、時間がかかる場合があります。
- **削除された stash は、ガベージコレクションが実行されるまで**の間のみ復元可能です。
- 重要な変更は定期的にコミットすることをお勧めします。
- stash は一時的な保存手段として使用するのが最適です。

### 参考

- [Git stash を復元する](https://zenn.dev/snowcait/articles/7ba0720db50aea28c652)
- [コミット前の内容を一時的に避けておく「git stash」の使い方](https://www.granfairs.com/blog/entry-3205/)
- [色々な git stash](https://qiita.com/akasakas/items/768c0b563b96f8a9be9d)
- [ATLASSIAN - git stash ](https://www.atlassian.com/ja/git/tutorials/saving-changes/git-stash)
- [あんまり知られていないけど、地味に便利な git コマンド](https://qiita.com/app_js/items/7ef0f2ab513d3de1471f)
- [変更を一時的に退避しよう!git stash を使いこなす 5 つのステップ](https://www.sejuku.net/blog/71428)
- [よく使ってよく忘れる git コマンド集](https://hakumai-no-otomo.hatenablog.com/entry/2020/10/05/%E3%82%88%E3%81%8F%E4%BD%BF%E3%81%A3%E3%81%A6%E3%82%88%E3%81%8F%E5%BF%98%E3%82%8C%E3%82%8Bgit%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E9%9B%86)
