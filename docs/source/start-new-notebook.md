
# Start working on a new notebook

1. Let's start a new notebook from JupyterLab console (or using the JupyterLab menu).

    <div style="text-align:center">
    <img alt="Start new notebook" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabStartNewNotebook.png">
    </div>

2. Run cell with `%horus check` to check the status of your notebook:

    <div style="text-align:center">
    <img alt="Horus check initial command" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabHorusCheckInitial.png">
    </div>

    As you can see, initially there are errors reported because no Pipfile or Pipfile.lock exist for this notebook.

3. Run cell with `%horus requirements --add <package-name>` to add a new package.

    For example, let's add a common package used in ML projects: `%horus requirements --add boto3`

    <div style="text-align:center">
    <img alt="Horus requirements add" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabHorusAdd.png">
    </div>

4. You can check the dependencies content of your notebook by running `%horus show`:

    <div style="text-align:center">
    <img alt="Horus show command after add" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabHorusShowAfterAdd.png">
    </div>

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

- [create dependencies for your existing notebook](./add-missing-dependencies-notebook.md)

- [convert notebook that uses pip commands in cells](./convert-notebook.md)

- [use a reproducible notebook](./run-reproducible-notebook.md)


## Next steps

[Remove kernels](./clean-kernel.md)
