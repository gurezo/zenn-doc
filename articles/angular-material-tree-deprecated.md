---
title: 'Angular Material TreeControl 廃止と移行の現状（2026）'
emoji: '✨'
type: 'idea' # tech: 技術記事 / idea: アイデア
topics: [Angular, Material, CDK]
published: true
---

:::message

### TreeControl 系の deprecated

:::

2025 年 05 月 29 日、Angular Material の Tree コンポーネントで使用される **FlatTreeControl** および **NestedTreeControl** が deprecated になっていることに気付きました。

本記事では、**2026 年 02 月 16 日時点での FlatTreeControl / NestedTreeControl の現状**を、Angular Material の GitHub Issue を元に整理します。

# FlatTreeControl の現状

![flat-tree-control](/images/angular-material-tree-deprecated/flat-tree-control.png)

- [cdk/tree/control/flat-tree-control.ts#L16-L23](https://github.com/angular/components/blob/main/src/cdk/tree/control/flat-tree-control.ts#L16-L23)
- **代替実装方法はまだ十分に整理されていません**
- 公式 examples や docs でも引き続き使用されています

| Issue                                                        | 内容                                  | 状況 |
| ------------------------------------------------------------ | ------------------------------------- | ---- |
| [#29856](https://github.com/angular/components/issues/29856) | deprecated 後の expand 方法が不明     | Open |
| [#29613](https://github.com/angular/components/issues/29613) | FlatTreeControl の代替方法            | Open |
| [#31524](https://github.com/angular/components/issues/31524) | examples が deprecated API を使用     | Open |
| [#29764](https://github.com/angular/components/issues/29764) | docs example が deprecated API を使用 | Open |

# NestedTreeControl の現状

![nested-tree-control](/images/angular-material-tree-deprecated/nested-tree-control.png)

- [cdk/tree/control/nested-tree-control.ts#L19-L26](https://github.com/angular/components/blob/main/src/cdk/tree/control/nested-tree-control.ts#L19-L26)
- NestedTreeControl も同様に deprecated になっていますが、**migration はまだ完了していません**

| Issue                                                        | 内容                              | 状況   |
| ------------------------------------------------------------ | --------------------------------- | ------ |
| [#29621](https://github.com/angular/components/issues/29621) | docs が deprecated API を使用     | Closed |
| [#31524](https://github.com/angular/components/issues/31524) | examples が deprecated API を使用 | Open   |
| [#29919](https://github.com/angular/components/issues/29919) | migration guide の提供要望        | Open   |

:::message alert

### 2026年02月16日時点の状況

:::

最新リリース：

[https://github.com/angular/components/releases/tag/v21.1.4](https://github.com/angular/components/releases/tag/v21.1.4)

この時点では、

**TreeControl 系の削除などの破壊的変更は実施されていません。**

つまり、

- deprecated ではあるものの
- **現時点では引き続き使用可能**

な状態です。

# なぜ migration が進んでいないのか

理由の一つは、**TreeControl が Tree コンポーネントの中核機能を担っているため**です。

TreeControl は以下の機能を提供しています

- expand
- collapse
- toggle
- expandAll
- collapseAll

これらの機能を新しい API：

- childrenAccessor
- levelAccessor
- expansionKey
- isExpanded

でどのように置き換えるかについて、

**公式として明確な migration パターンがまだ十分に確立されていません。**

# 今 migration すべきか？

:::message alert

### 結論：現時点では急いで対応する必要はありません

:::

- migration guide がまだ不十分
- 公式 examples でも deprecated API が使用されている
- Angular Material チーム自身も migration を進めている段階のため

# まとめ

2026 年 02 月 16 日時点の状況

- FlatTreeControl / NestedTreeControl は deprecated
- 将来のバージョンで削除予定
- ただし現時点では削除されていない
- migration 方法はまだ完全には整理されていない
- 現時点では継続して使用可能

今後 migration guide や examples の更新が進む可能性があるため、Angular Material のリリース情報を継続的に確認することをおすすめします。
