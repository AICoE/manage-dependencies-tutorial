# Bring your notebook and make it reproducible (Convert cells with pip commands automatically)

Let's say I have a notebook I was working on that uses `pip` in my cells and I want to make it reproducible.

1. Let's open the notebook called `make-notebook-reproducible`, provided in `notebooks` folder.

    <div style="text-align:center">
    <img alt="Start my notebook with pip cells" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabStartExistingNotebookPip.png">
    </div>

    NOTE: _A warning from the jupyterlab-requirements extension will appear to tell users what should be used to handle dependencies._

    <div style="text-align:center">
    <img alt="Start my notebook and warning" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabStartExistingNotebookPipWarning.png">
    </div>

2. Run cell with `%horus check` to check the status of your notebook:

    <div style="text-align:center">
    <img alt="Horus check initial command" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabHorusCheckInitialPip.png">
    </div>

    As you can see, initially there are errors reported because no Pipfile or Pipfile.lock exist for this notebook.

3. Run `%horus convert`, so that the extenstion can convert `!pip install` cells to commands that allow reproducibility.

    <div style="text-align:center">
    <img alt="Horus convert command" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabHorusConvert.png">
    </div>

4. Run the converted cells to add the requirements to your notebook.

    NOTE: _If you want to edit some dependencies, you can simply add them again with your specific requirements (`%horus requirement --add`)._

5. Run cell with `%horus check` to check the status of your notebook.


6. Run `%horus lock` to lock dependencies using Thoth resolution engine.

    If you are interested in a specific recommendation from Thoth, add `--recommendation-type <recommendation-type>`, default is `latest` ("latest", "stable", "performance", "security").

    By default, Thoth will discover the runtime environment you are running on. If you want to receive a recommendation for a specific runtime environment, you can use the following flags:

    - `--os-name`
    - `--os-version`
    - `--python-version`

    You can also use `%horus lock --pipenv` if you want to lock dependencies with Pipenv resolution engine.

7. Run cell with `%horus check` to check the status of your notebook or `%horus show` to show the content of your notebook.

    If you want to show a specific part of your dependencies information stored in the notebook metadata, you can use the following flags:

    - `--pipfile`
    - `--pipfile-lock`
    - `--thoth-config` (only if Thoth resolution engine was used)


## Other cases

You can consider another use case for managing dependencies:

- [start working on a new notebook](./start-new-notebook.md)

- [create dependencies for your existing notebook](./add-missing-dependencies-notebook.md)

- [use a reproducible notebook](./run-reproducible-notebook.md)


## Next steps

[Remove kernels](./clean-kernel.md)
