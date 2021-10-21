# Reproducibility of Jupyter Notebooks

Reproducibility and shareability of notebooks is very important if you want to allow others to repeat your experiments and avoid issues due to dependencies management.
When using `pip install <package_name>` is not possible to verify which software stack was used to run the notebook and therefore another user cannot repeat the same experiment.
Dependency management is one of the most important requirements for reproducibility. Having dependencies clearly stated allows portability of notebooks, so they can be shared safely with others, reused in other projects or simply reproduced. If you want to know more about this issue in the data science domain, have a look at this [article](https://developers.redhat.com/blog/2021/03/19/managing-python-dependencies-with-the-thoth-jupyterlab-extension/) or this [video](https://www.youtube.com/watch?v=ifyQ2oSxjnU).

In order to help developers (including data scientists), dependencies for Jupyter notebooks in this tutorial are managed using the JupyterLab extension [jupyterlab-requirements][1].

You can use this extension for each of your notebook to guarantee they have the correct dependencies. This extension is able to add/remove dependencies, lock them and store them in the notebook metadata. In this way all the dependencies information required to repeat the environment are shipped with the notebook.

In particular, the following notebook metadata is created for you, when you use Thoth's dependency management tool:

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

- using the `horus` CLI directly from terminal or integrated in pipelines (check the [video](https://www.youtube.com/watch?v=fW0YKugL26g&t) or this [link](https://github.com/thoth-station/jupyterlab-requirements#horus-jupyterlab-requirements-cli) if you want to know more about it).

<div style="text-align:center">
<img alt="JupyterLab Requirements Horus CLI" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabRequirementsExtensionCLI.png">
</div>

- using the `Manage Dependencies` button that appears in the notebook when it is opened (check the [link](https://github.com/thoth-station/jupyterlab-requirements#extension-button) if you want to know more about it):

<div style="text-align:center">
<img alt="JupyterLab Requirements UI" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabRequirementsExtension.jpg">
</div>

NOTE:_In this tutorial we will focus on %horus magic commands._

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

You can also use `%horus lock --pipenv` if you want to lock dependencies with Pipenv resolution engine.

6. Run cell with `%horus check` to check the status of your notebook or `%horus show` to show the content of your notebook.

If you want to show a specific part of your dependencies information stored in the notebook metadata, you can use the following flags:

- `--pipfile`
- `--pipfile-lock`
- `--thoth-config` (only if Thoth resolution engine was used)


### Bring your notebook and make it reproducible

We will consider two use cases:

- This is a notebook I was working on and I want to make it reproducible because I did not state any dependencies.

- This is a notebook I was working on that uses `pip` in my cells and I want to make it reproducible.

#### Notebook with no commands for dependency management

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


#### Notebook with pip install cells

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

<div style="text-align:center">
<img alt="Horus check after discover" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabHorusCheckAfterDiscover.png">
</div>

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

### Reproducible Notebooks

This section is intended for users who would like to manage already reproducible notebooks.

NOTE: _In order to set up your reproducible notebook environment, you have to verify that your [JupyterLab](https://github.com/thoth-station/jupyterlab-requirements#requirements) and your [jupyterlab-requirements](https://github.com/thoth-station/jupyterlab-requirements/blob/master/requirements.txt) versions are both up to date._

#### Create a new kernel with %horus

To verify that the notebook is set to the new kernel, run ```%horus set-kernel``` to make sure you have a kernel with your dependencies installed. You can also assign a new name to your kernel using ```--kernel-name```.

You can see what is the current kernel for you rnotebook using the top right button : 

<div style="text-align:center">
<img alt="Current kernel button" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabSelectKernelButton.png">
</div>

<div style="text-align:center">
<img alt="Select kernel button" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabSelectKernel.png">
</div>


## Next Step

[Push changes to GitHub](./push-changes.md)

## References

* [jupyterlab-requirements][1]

[1]: https://github.com/thoth-station/jupyterlab-requirements
