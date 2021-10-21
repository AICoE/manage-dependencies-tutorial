# Run reproducible notebook

Let's say I have a reproducible notebook that someone shared with me. This section is intended for users who would like to manage already reproducible notebooks.

NOTE: _In order to set up your reproducible notebook environment, you have to verify that your [JupyterLab](https://github.com/thoth-station/jupyterlab-requirements#requirements) and your [jupyterlab-requirements](https://github.com/thoth-station/jupyterlab-requirements/blob/master/requirements.txt) versions are both up to date._

## Create a new kernel with %horus

To verify that the notebook is set to the new kernel, run ```%horus set-kernel``` to make sure you have a kernel with your dependencies installed. You can also assign a new name to your kernel using ```--kernel-name``` flag.

You can see what is the current kernel for your notebook using the top right button:

<div style="text-align:center">
<img alt="Current kernel button" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabSelectKernelButton.png">
</div>

<div style="text-align:center">
<img alt="Select kernel button" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabSelectKernel.png">
</div>

## Other cases

You can consider another use case for managing dependencies:

- [start working on a new notebook](./start-new-notebook.md)

- [create dependencies for your existing notebook](./add-missing-dependencies-notebook.md)

- [convert notebook that uses pip commands in cells](./convert-notebook.md)


## Next steps

[Remove kernels](./clean-kernel.md)
