
# Bring your notebook and make it reproducible (Discover dependencies required automatically)

Let's say I have a notebook I was working on and I want to make it reproducible because I did not state any dependencies.

1. Let's open the notebook called `discover-my-notebook`, provided in `notebooks` folder.

    <div style="text-align:center">
    <img alt="Start my notebook" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabStartExistingNotebook.png">
    </div>

2. Run cell with `%horus check` to check the status of your notebook:

    <div style="text-align:center">
    <img alt="Horus check initial command" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabHorusCheckInitialDiscover.png">
    </div>

    As you can see, initially there are errors reported because no Pipfile or Pipfile.lock exist for this notebook.

3. Run `%horus discover`, so that Thoth can discover the packages that you are using in your dependencies

    <div style="text-align:center">
    <img alt="Horus discover command" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabHorusDiscover.png">
    </div>

    As you can notice the `%horus discover` command is able to read the content of your notebook and identify packages that are actually used in the notebook. `numpy` for example is imported but never used, therefore is not added to the requirements. The library that is able to identify libraries is called `invectio`, have a look [here](https://github.com/thoth-station/invectio) if you want to know more.

    NOTE: _If you want to edit some dependencies, you can simply add them again with your specific requirements (`%horus requirement --add`)._

4. Run cell with `%horus check` to check the status of your notebook.

5. Run `%horus lock` to lock dependencies using Thoth resolution engine.

    If you are interested in a specific recommendation from Thoth, add `--recommendation-type <recommendation-type>`, default is `latest` ("latest", "stable", "performance", "security").

    By default, Thoth will discover the runtime environment you are running on. If you want to receive a recommendation for a specific runtime environment, you can use the following flags:

    - `--os-name`
    - `--os-version`
    - `--python-version`

    You can also use `%horus lock --pipenv` if you want to lock dependencies with Pipenv resolution engine.

6. Run cell with `%horus check` to check the status of your notebook or `%horus show` to show the content of your notebook.

    If you want to show a specific part of your dependencies information stored in the notebook metadata, you can use the following flags:

    - `--pipfile`
    - `--pipfile-lock`
    - `--thoth-config` (only if Thoth resolution engine was used)


## Other cases

You can consider another use case for managing dependencies:

- [start working on a new notebook](./start-new-notebook.md)

- [convert notebook that uses pip commands in cells](./convert-notebook.md)

- [use a reproducible notebook](./run-reproducible-notebook.md)


## Next steps

[Remove kernels](./clean-kernel.md)
