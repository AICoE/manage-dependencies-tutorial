# Setup initial environment

The environment that will be used for this tutorial is an open environment with open source technologies running on [Red Hat Openshift][1] on an open infrastructure with an open community that allow developers and operators to collaborate and learn from each other, called [Operate First][2].
[Operate First][2] hosts [Open Data Hub][3] with all the tools provided for Data Science projects (e.g. JupyterHub, Elyra, Kubeflow Pipelines, Seldon, Prometheus, Grafana, Superset) running on [Red Hat Openshift][1].

## Fork this repo from GitHub

To begin, you'll need to fork this repository to create your own copy. If you're unsure how, look at [Fork a Repo](https://docs.github.com/en/github/getting-started-with-github/fork-a-repo) from GitHub docs.


## Select one the following options to run the tutorial

- Use [Project Meteor][5] (suggested way);

- Use [JupyterHub][4];

- Use a container image locally.


### Use Project Meteor

[Project Meteor][5] is a combined effort across the AICoE team at Red Hat, to provide a single tool for data scientists and other users where they can interact with, explore and leverage all of our services, tools and technologies for developing intelligent applications. [Project Meteor][5] is deployed on [Operate First][2] and you can use it following this [link](https://shower.meteor.zone/)


1. Enter the URL to your Git repository in [Project Meteor](https://shower.meteor.zone/.

<div style="text-align:center">
<img alt="Enter URL Project Meteor" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/ProjectMeteorEnterURL.png">
</div>

[Project Meteor][5] on the background will create two images for you:

- JupyterBook where you can view easily shareable, and rendered high-quality static content from experiment.

- A live JupyterLab environment where you can interact with your project and run your experiments.

You can track errors and status of the pipelines using the `Show details` link:

<div style="text-align:center">
<img alt="Project Meteor Show details" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/ProjectMeteorShowDetails.png">
</div>

Once everything is ready, you can access the image to run the tutorial using `Open as JupyterHub` link on the bottom, while you can access the JupyterBook using `Open as Website` link on the bottom.

<div style="text-align:center">
<img alt="Project Meteor Show details" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/ProjectMeteorShowDetails.png">
</div>

Now you are all set to start the tutorial.


### (ALTERNATIVE) Access the Elyra image in JupyterHub

In order to access the [JupyterHub][4] from [Open Data Hub][3] deployed on the [Operate First][2] cluster:

1. Click this [link](https://jupyterhub-opf-jupyterhub.apps.smaug.na.operate-first.cloud/) to visit the Operate First JupyterHub.

    <div style="text-align:center">
    <img alt="Jupyter Hub UI" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterHubNewUI.png">
    </div>

2. Select the image called `Experimental Elyra Notebook Image` from the JupyterHub spawner.

3. Select `Large` for container size.


#### Clone your repo using Jupyterlab Git Extension

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


### (ALTERNATIVE) Run the tutorial image locally (ALTERNATIVE)

PRE-REQUISITE: Make sure you have [podman](https://podman.io/) installed:

1. Run the following command:

```
podman run -p 8888:8888 quay.io/thoth-station/manage-dependencies-tutorial:latest start-singleuser.sh --ip="0.0.0.0" --port=8888
```


## Next Step

[Manage dependencies for your notebook](./manage-dependencies-notebook.md)


## References

* [Red Hat Openshift][1]
* [Operate First][2]
* [Open Data Hub][3]
* [JupyterHub][4]
* [Project Meteor][5]

[1]: https://www.openshift.com/
[2]: https://www.operate-first.cloud/
[3]: https://opendatahub.io/
[4]: https://jupyter.org/hub
[5]: https://github.com/AICoE/meteor
