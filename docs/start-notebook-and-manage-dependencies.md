# Reproducibility of Jupyter Notebooks

Reproducibility and shareability of notebooks is very important if you want to allow others to repeat your experiments and avoid issues due to dependencies management.
When using `pip install <package_name>` is not possible to verify which software stack was used to run the notebook and therefore another user cannot repeat the same experiment.
Check the video [here](https://www.youtube.com/watch?v=ifyQ2oSxjnU) if you want to know more.

In order to avoid this issues, dependencies for Jupyter notebooks in this tutorial are managed using the JupyterLab extension [jupyterlab-requirements][1].

You can use this extension for each of your notebook to guarantee they have the correct dependencies. This extension is able to add/remove dependencies, lock them and store them in the notebook metadata. In this way all the dependencies information required to repeat the environment are shipped with the notebook.

In particular, in the notebook metadata you will find:

- `requirements (Pipfile)`;

- `requirements lock with all versions and hashes (Pipfile.lock)`;

- `dependency resolution engine` used (Thoth or Pipenv);

- `.thoth.yaml configuration file` (only for Thoth resolution engine).

All this information can allow reproducibility and shareability of the notebook.


## Manage dependencies with the jupyterlab-requirements extension

There are 3 ways to interact with [jupyterlab-requirements][1] JupyterLab extension:

- using `%horus` magic commands directly in your notebook's cells (preferred approach). To learn more about how to use the `%horus` magic commands check out the guide [here](https://github.com/thoth-station/jupyterlab-requirements#horus-magic-command) or the video [here](https://www.youtube.com/watch?v=FjVxNTXO70I)

<div style="text-align:center">
<img alt="JupyterLab Requirements Horus magic commands" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabRequirementsExtensionMC.png">
</div>

- using the `horus` CLI directly from terminal or integrated in pipelines ([check video](https://www.youtube.com/watch?v=fW0YKugL26g&t)).

<div style="text-align:center">
<img alt="JupyterLab Requirements Horus CLI" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabRequirementsExtensionCLI.png">
</div>

- using the `Manage Dependencies` button that appears in the notebook when it is opened:

<div style="text-align:center">
<img alt="JupyterLab Requirements UI" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabRequirementsExtension.jpg">
</div>


### Start working on a new notebook

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

6. Run cell with `%horus check` to check the status of your notebook or `%horus show` to show the content of your notebook.

If you want to show a specific part of your dependencies information stored in the notebook metadata, you can use the following flags:

- `--pipfile`
- `--pipfile-lock`
- `--thoth-config` (only if Thoth resolution engine was used)


### Bring your notebook and make it reproducible

1. Let's open the notebook `my-notebook` provided in `notebooks` folder.

<div style="text-align:center">
<img alt="Start my notebook" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabStartExistingNotebook.png">
</div>

This is a notebook I was working on and I want to make it reproducible because I did not state any dependencies.

NOTE: _If you have a notebook with `!pip install <package-name>` cells, they will be removed and converted to commands that allow reproducibility once you start the notebook._

2. Run `%horus discover`, so that Thoth can discover the packages that you are using in your dependencies

<div style="text-align:center">
<img alt="Horus discover command" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabHorusDiscover.png">
</div>

As you can notice the `%horus discover` command is able to read the content of your notebook and identify packages that are actually used in the notebook. `numpy` for example is imported but never used, therefore is not added to the requirements. The library that is able to identify libraries is called `invectio`, have a look [here](https://github.com/thoth-station/invectio) if you want to know more.

NOTE: _If you want to edit some dependencies, you can simply add them again with your specific requirements (`%horus requirement --add`)._

3. Run cell with `%horus check` to check the status of your notebook.

<div style="text-align:center">
<img alt="Horus check after discover" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabHorusCheckAfterDiscover.png">
</div>

4. Run `%horus lock` to lock dependencies using Thoth resolution engine.

<div style="text-align:center">
<img alt="Horus lock command" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabHorusLock.png">
</div>

If you are interested in a specific recommendation from Thoth, add `--recommendation-type <recommendation-type>`, default is `latest` ("latest", "stable", "performance", "security").

By default, Thoth will discover the runtime environment you are running on. If you want to receive a recommendation for a specific runtime environment, you can use the following flags:

- `--os-name`
- `--os-version`
- `--python-version`

5. Run cell with `%horus check` to check the status of your notebook or `%horus show` to show the content of your notebook.

If you want to show a specific part of your dependencies information stored in the notebook metadata, you can use the following flags:

- `--pipfile`
- `--pipfile-lock`
- `--thoth-config` (only if Thoth resolution engine was used)


## Next Step

[Push changes to GitHub](./push-changes.md)

## References

* [jupyterlab-requirements][1]

[1]: https://github.com/thoth-station/jupyterlab-requirements
