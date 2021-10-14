# Setup initial environment

The environment that will be used for this tutorial is an open environment with open source technologies running on [Red Hat Openshift][1] on an open infrastructure with an open community that allow developers and operators to collaborate and learn from each other, called [Operate First][2].
[Operate First][2] hosts [Open Data Hub][3] with all the tools provided for Data Science projects (e.g. JupyterHub, Elyra, Kubeflow Pipelines, Seldon, Prometheus, Grafana, Superset) running on [Red Hat Openshift][1].

## 1. Fork this repo from GitHub

To begin, you'll need to fork this repository to create your own copy. If you're unsure how, look at [Fork a Repo](https://docs.github.com/en/github/getting-started-with-github/fork-a-repo) from GitHub docs.


## 2. Access the Elyra image in JupyterHub

In order to access the [JupyterHub][4] from [Open Data Hub][3] deployed on the [Operate First][2] cluster:

1. Click this [link](https://jupyterhub-opf-jupyterhub.apps.smaug.na.operate-first.cloud/) to visit the Operate First JupyterHub.

    <div style="text-align:center">
    <img alt="Jupyter Hub UI" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterHubNewUI.png">
    </div>

2. Select the image called `Experimental Elyra Notebook Image` from the JupyterHub spawner.

3. Select `Large` for container size.


## 3. Clone your repo using Jupyterlab Git Extension

Once your image is ready and you are in the Jupyterlab UI, you can use the Git extension provided to clone this repo.

1. Click the Git extension button from Jupyterlab UI:

    <div style="text-align:center">
    <img alt="Look for Git extension button" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabGitExtension.png">
    </div>

2. Take HTTPS link of the GitHub repo you want to clone, for this tutorial use your forked one from this repo:

    <div style="text-align:center">
    <img alt="Take link from forked repo" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/TakeLinkForkedRepo.png">
    </div>

3. Insert the link taken from your forked repo in the JupyterLab Git Extension: e.g. `https://github.com/AICoE/manage-dependencies-tutorial.git`

    <div style="text-align:center">
    <img alt="Clone your repo" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabCloneYourRepo.png">
    </div>


## Next Step

[Manage dependencies for your notebook](./start-notebook-and-manage-dependencies.md)


## References

* [Red Hat Openshift][1]
* [Operate First][2]
* [Open Data Hub][3]
* [JupyterHub][4]

[1]: https://www.openshift.com/
[2]: https://www.operate-first.cloud/
[3]: https://opendatahub.io/
[4]: https://jupyter.org/hub
