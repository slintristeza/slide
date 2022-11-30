---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS
css: unocss
---

# そのレコードの主キーに連番を使うのをやめてみよう

---
layout: center
---

# 主キーとは

---

# 主キーとは

こんなやつ
![img](/img1.png)

---

# 主キーとは

- 必須
- 値が重複しない
- そのフィールドを使ってレコードを取得したり、更新時のキーにするもの

---
layout: center
---

# 連番のデメリット

---

# 連番のデメリット

## 重複

タイミングによっては値が被り、エラーを起こす

- 同じタイミングでレコード登録
- サーバーの処理のタイミングなど

---

# 連番のデメリット

## ルックアップで不整合が起きる

例えば以下のような流れ

1. アプリAでID 0001, 名称 商品Aのレコード作成
2. アプリBでID 0001のレコードをルックアップして参照する
3. アプリAでID 0001のレコードを削除
4. アプリAでID 0001, 名称 商品Bのレコードを作成
5. アプリBではルックアップを再取得するまで商品Aのままとなる

---

# 連番のデメリット

## 外部に公開するデータの場合、番号をずらせば他人のIDや番号を用意に推測可能

- 会員番号0001のようなIDで外部からデータを取得できる場合、0002,0003と変えていけば総当りで全会員のデータが取得可能

---
layout: center
---

# 連番にしてもいいケース

---

# 連番にしてもいいケース

## 主キーにせず、ソートキーとして利用する場合

- レコードの主キーは連番にしない
- 連番のフィールドは主キーとは別にする
- この場合は値の重複は可能にしてもいい気がする

---

# 連番にしてもいいケース

## 他システムとの連携が必要で他システムの主キーが連番になっている場合

- 他システムのキー(連番)を保持するフィールドとkintoneでの主キー(連番ではない)を分けたほうが良い

---
layout: center
---

# 連番がダメならどうするか

---

# 連番がダメならどうするか

## プログラムで8~12文字ぐらいのランダムな英数字を生成しましょう

- 数字 + 英字(大文字)のみでも重複する可能性は低い
- 生成可能なパターンの計算式
- 10(0~9の数字) + 26(アルファベットの文字数) ^ 桁数
- 8桁で2,821,109,907,456 -> 2兆8000億
- 10桁で3,656,158,440,062,980 -> 3650兆

---

# 連番がダメならどうするか

## 他のシステムだとどうしているか

- slackは8桁(ワークスペース内での主キーだと思う)
- LINEは33桁(先頭のみ大文字？)
