# Setup initial environment


## 1. Fork this repo from GitHub

To begin, you'll need to fork this repository to create your own copy. If you're unsure how, look at [Fork a Repo](https://docs.github.com/en/github/getting-started-with-github/fork-a-repo) from GitHub docs.


## 2. Access the Elyra image in JupyterHub

In order to access the [JupyterHub][3] deployed on the [Operate First][4] cluster:

1. Click this [link](https://jupyterhub-opf-jupyterhub.apps.zero.massopen.cloud/) to visit the Operate First JupyterHub.

    <div style="text-align:center">
    <img alt="Jupyter Hub UI" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterHubNewUI.png">
    </div>

2. Select the image called `Experimental Elyra Notebook Image` from the JupyterHub spawner.

3. Select `Large` for container size.


## 3. Clone your repo using Jupyterlab Git Extension

Once your image is ready and you are in the Jupyterlab UI, you can use the Git extension provided to clone this repo.

1. Click the Git extension button from Jupyterlab UI:

    <div style="text-align:center">
    <img alt="Look for Git extension button" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/ElyraGitExtension.png">
    </div>

2. Take HTTPS link of the GitHub repo you want to clone, for this tutorial use your forked one from this repo:

    <div style="text-align:center">
    <img alt="Take link from forked repo" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/TakeLinkForkedRepo.png">
    </div>

3. Insert the link taken from your forked repo in the JupyterLab Git Extension: e.g. `https://github.com/AICoE/manage-dependencies-tutorial.git`

    <div style="text-align:center">
    <img alt="Clone your repo" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/CloneYourRepo.png">
    </div>


## Next Step

[Manage dependencies for your notebook](./start-notebook-and-manage-dependencies.md)


## References

* [Project template][1]
* [Project Meteor][2]
* [JupyterHub][3]
* [Operate First][4]

[1]: https://github.com/aicoe-aiops/project-template
[2]: https://github.com/AICoE/meteor
[3]: https://jupyter.org/hub
[4]: https://www.operate-first.cloud/
