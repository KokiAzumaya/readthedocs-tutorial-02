例：Read the Docs 用の多言語対応 MkDocs プロジェクト
=====================================================

このプロジェクトは、[Read the Docs 用の基本的な MkDocs の例](https://github.com/readthedocs-examples/example-mkdocs-basic) をもとに、ドキュメントを英語と日本語で公開できるように拡張したものです。Read the Docs を初めて使う場合は、公式の [Read the Docs チュートリアル](https://docs.readthedocs.io/en/stable/tutorial/index.html) をご覧ください。

📚 `docs/en/` と `docs/ja/`<br>
英語のドキュメントは `docs/en/` に、その日本語訳は `docs/ja/` にあります。すべての `*.md` がドキュメントの各セクションになります。日本語のファイルは手で書きます。Read the Docs の言語切り替えで同じページに移動できるよう、ファイル名と構成は英語版と同じにしてください。

⚙️ `.readthedocs.yaml`<br>
Read the Docs のビルド設定は `.readthedocs.yaml` に書かれています。英語用と日本語用の Read the Docs プロジェクトは、このファイルを共有しています。各ビルドでは、プロジェクトの言語設定（`en` または `ja`）が入る `$READTHEDOCS_LANGUAGE` によって、使う MkDocs の設定ファイルを選びます。

⚙️ `mkdocs.base.yml`、`mkdocs.en.yml`、`mkdocs.ja.yml`<br>
全言語に共通する [MkDocs の設定](https://www.mkdocs.org/user-guide/configuration/) は `mkdocs.base.yml` に書かれています。MkDocs と Markdown の拡張機能もいくつか含まれています。`mkdocs.en.yml` と `mkdocs.ja.yml` には言語ごとの設定だけが書かれていて、`INHERIT` で `mkdocs.base.yml` を読み込みます。拡張機能やテーマなど、独自の設定は `mkdocs.base.yml` に追加してください。多くの拡張機能やテーマでは、追加の Python パッケージのインストールが必要になることに注意してください。

📍 `docs/requirements.txt` と `docs/requirements.in`<br>
Python の依存パッケージは、ここで[バージョンを固定](https://docs.readthedocs.io/en/latest/guides/reproducible-builds.html)しています（[pip-tools](https://pip-tools.readthedocs.io/en/latest/) を使用）。Python の依存パッケージは `requirements.txt` に追加してください。[pip-tools](https://pip-tools.readthedocs.io/en/latest/) を使う場合は、`docs/requirements.in` を編集し、`pip-compile docs/requirements.in` を忘れずに実行してください。

💡 `docs/en/api.md`<br>
API リファレンスを自動生成するために、例として Python モジュール `lumache` を追加しています。これには `:::` 記法を使います。詳しくは [mkdocstrings のドキュメント](https://mkdocstrings.github.io/) をご覧ください。

💡 `docs/en/usage.md`<br>
API リファレンスの関数への直接リンクや、例の関数 `lumache.get_random_ingredients` のドキュメントの埋め込みも含めています。この機能も [mkdocstrings](https://mkdocstrings.github.io/python/) 拡張機能によるものです。

💡 `lumache.py`<br>
この例の Python モジュールの API ドキュメントは自動生成されます。*docstring* をそのままドキュメントに使っているので、表示されたドキュメントにどう反映されるかを見てみてください。docstring には [Sphinx 形式](https://pythonhosted.org/an_example_pypi_project/sphinx.html#function-definitions) を使っていますが、`mkdocs.base.yml` を編集して `google` や `numpy` に変更することもできます。

📜 `README.md` と `README.ja.md`<br>
`README.md` の内容は、GitHub に表示されるほか、英語版ドキュメントのトップページ（`docs/en/index.md`）にも取り込まれています。その日本語訳の `README.ja.md` は、日本語版ドキュメントのトップページ（`docs/ja/index.md`）に取り込まれています。


この例のプロジェクトの使い方
---------------------

このプロジェクトは標準的な MkDocs の構成になっていて、Read the Docs でも、ローカル（自分のノート PC）でビルドするのとほぼ同じ方法でビルドされます。

このドキュメントプロジェクトは、ローカルでビルドして表示できます。先に [Python の仮想環境を有効にする](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment) ことをおすすめします。

```console
# 必要な Python の依存パッケージ（MkDocs など）をインストールする
pip install -r docs/requirements.txt

# MkDocs の開発用サーバーを起動する（英語）
mkdocs serve -f mkdocs.en.yml

# MkDocs の開発用サーバーを起動する（日本語）
mkdocs serve -f mkdocs.ja.yml
```

この例を自分のプロジェクトで使う
-------------------------------------

Read the Docs を初めて使う場合は、[Read the Docs のユーザードキュメント](https://docs.readthedocs.io/) を参照してください。

ドキュメント作成を始めるためにこのコードをコピーする場合は、次の作業が必要です。

1. `docs/` フォルダを Python プロジェクトと同じ場所に置く。新しいプロジェクトを始める場合は、例の `pyproject.toml` の設定を応用できます。
1. 既存のリポジトリを使うか、GitHub、GitLab、Bitbucket など Read the Docs が対応しているホスティングサービスで新しいリポジトリを作る。
1. `mkdocs.base.yml`、`mkdocs.en.yml`、`mkdocs.ja.yml`、`.readthedocs.yaml`、`docs/` フォルダを自分のプロジェクトにコピーする。
1. すべてのファイルをカスタマイズし、例の内容を置き換える。
1. ローカルでドキュメントをビルドし直し、動くことを確認する。
1. *最後に*、Read the Docs にプロジェクトを登録する。[ドキュメントのインポート](https://docs.readthedocs.io/en/stable/intro/import-guide.html) を参照してください。
1. 同じリポジトリを 2 つ目のプロジェクトとしてもう一度登録し、言語を日本語に設定する。
1. 英語用プロジェクトの *Settings > Translations* で、日本語用プロジェクトを翻訳として追加する。


Read the Docs チュートリアル
----------------------

Read the Docs を始めるには、[Read the Docs チュートリアル](https://docs.readthedocs.io/en/stable/tutorial/) も参考にしてください。このリポジトリと同じような例のプロジェクトをビルドする手順を、最初から最後まで説明しています。
