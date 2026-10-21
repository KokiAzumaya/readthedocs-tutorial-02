Example: Multilingual MkDocs project for Read the Docs
=====================================================

This project is based on the [basic MkDocs example for Read the Docs](https://github.com/readthedocs-examples/example-mkdocs-basic), extended to publish the documentation in English and Japanese. If you are using Read the Docs for the first time, have a look at the official [Read the Docs Tutorial](https://docs.readthedocs.io/en/stable/tutorial/index.html).

📚 `docs/en/` and `docs/ja/`<br>
The English documentation lives in `docs/en/`, and its Japanese translation lives in `docs/ja/`. All the `*.md` make up sections in the documentation. The Japanese files are written by hand, and must have the same file names and structure as the English ones, so that the language switcher on Read the Docs can move between the same pages.

⚙️ `.readthedocs.yaml`<br>
Read the Docs Build configuration is stored in `.readthedocs.yaml`. The English and Japanese Read the Docs projects share this file. Each build selects the MkDocs configuration file by `$READTHEDOCS_LANGUAGE`, which is set from the project's language setting (`en` or `ja`).

⚙️ `mkdocs.base.yml`, `mkdocs.en.yml` and `mkdocs.ja.yml`<br>
The [MkDocs configuration](https://www.mkdocs.org/user-guide/configuration/) shared by all languages is stored in `mkdocs.base.yml`, including a few extensions for MkDocs and Markdown. `mkdocs.en.yml` and `mkdocs.ja.yml` contain only the language-specific settings, and load `mkdocs.base.yml` with `INHERIT`. Add your own configurations, such as extensions and themes, to `mkdocs.base.yml`. Remember that many extensions and themes require additional Python packages to be installed.

📍 `docs/requirements.txt` and `docs/requirements.in`<br>
Python dependencies are [pinned](https://docs.readthedocs.io/en/latest/guides/reproducible-builds.html) (uses [pip-tools](https://pip-tools.readthedocs.io/en/latest/)) here. Make sure to add your Python dependencies to `requirements.txt` or if you choose [pip-tools](https://pip-tools.readthedocs.io/en/latest/), edit `docs/requirements.in` and remember to run `pip-compile docs/requirements.in`.

💡 `docs/en/api.md`<br>
We add our example Python module `lumache` in order to auto-generate an API reference. To do this, we use the `:::` syntax, you can read more in the [mkdocstrings documentation](https://mkdocstrings.github.io/).

💡 `docs/en/usage.md`<br>
We also include some direct links to a function from the API reference, as well as embedding documentation for the example function `lumache.get_random_ingredients`. This functionality is also from the [mkdocstrings](https://mkdocstrings.github.io/python/) extension.

💡 `lumache.py`<br>
API docs are generated for this example Python module - they use *docstrings* directly in the documentation, notice how this shows up in the rendered documentation. We use the [Sphinx convention](https://pythonhosted.org/an_example_pypi_project/sphinx.html#function-definitions) for docstrings, however you are free to edit `mkdocs.base.yml` to change this option to `google` or `numpy`.

📜 `README.md` and `README.ja.md`<br>
Contents of `README.md` are visible on GitHub and included on the English documentation index page (`docs/en/index.md`). Its Japanese translation `README.ja.md` is included on the Japanese documentation index page (`docs/ja/index.md`).


Example Project usage
---------------------

This project has a standard MkDocs layout which is built by Read the Docs almost the same way that you would build it locally (on your own laptop!).

You can build and view this documentation project locally - we recommend that you activate [a local Python virtual environment first](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment):

```console
# Install required Python dependencies (MkDocs etc.)
pip install -r docs/requirements.txt

# Run the mkdocs development server (English)
mkdocs serve -f mkdocs.en.yml

# Run the mkdocs development server (Japanese)
mkdocs serve -f mkdocs.ja.yml
```

Using the example in your own project
-------------------------------------

If you are new to Read the Docs, you may want to refer to the [Read the Docs User documentation](https://docs.readthedocs.io/).

If you are copying this code in order to get started with your documentation, you need to:

1. place your `docs/` folder alongside your Python project. If you are starting a new project, you can adapt the `pyproject.toml` example configuration.
1. use your existing project repository or create a new repository on GitHub, GitLab, Bitbucket or another host supported by Read the Docs.
1. copy `mkdocs.base.yml`, `mkdocs.en.yml`, `mkdocs.ja.yml`, `.readthedocs.yaml` and the `docs/` folder into your project.
1. customize all the files, replacing example contents.
1. Rebuild the documentation locally to see that it works.
1. *Finally*, register your project on Read the Docs, see [Importing Your Documentation](https://docs.readthedocs.io/en/stable/intro/import-guide.html).
1. Register the same repository once more as a second project, and set its language to Japanese.
1. In the English project, go to *Settings > Translations* and add the Japanese project as a translation.


Read the Docs tutorial
----------------------

To get started with Read the Docs, you may also refer to the [Read the Docs tutorial](https://docs.readthedocs.io/en/stable/tutorial/). It provides a full walk-through of building an example project similar to the one in this repository.
