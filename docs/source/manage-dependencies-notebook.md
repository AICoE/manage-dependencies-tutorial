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

## Next steps

You can consider the use case you are interested in for managing dependencies:

- [start working on a new notebook](./start-new-notebook.md)

- [create dependencies for your existing notebook](./add-missing-dependencies-notebook.md)

- [convert notebook that uses pip commands in cells](./convert-notebook.md)

- [use a reproducible notebook](./run-reproducible-notebook.md)


## References

* [jupyterlab-requirements][1]

[1]: https://github.com/thoth-station/jupyterlab-requirements
