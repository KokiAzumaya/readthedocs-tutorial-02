使い方
=====

インストール
------------

Lumache を使うには、まず pip でインストールします:

```console
(.venv) $ pip install lumache
```

レシピを作る
----------------

ランダムな調味料のリストを取得する場合は、関数
`lumache.get_random_ingredients()` が使えます:

::: lumache.get_random_ingredients
    options:
      show_root_heading: true

<br>

`kind` パラメータは `"meat"`, `"fish"`, `"veggies"` のいずれかである必要があります。
そうでない場合は、 [`get_random_ingredients`][lumache.get_random_ingredients] が
例外 [`lumache.InvalidKindError`](/api#lumache.InvalidKindError) を発生させます。

例:

```python
>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']
```
