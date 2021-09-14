# Thoth Tutorial - manage your dependencies in Jupyter notebooks.

This tutorial is used to show how to manage dependencies for Jupyter Notebooks using Python to allow reproducibility and shareability.

Even though many developers (including data scientists) focus on their core problems when working on their experiments, there is one aspect that can make these projects not reusable.
One of the first steps during the development of a project is the `selection of libraries or dependencies`. When someone runs `pip install <package-name>`, they might not be aware that along with the library that is going to be installed, a direct dependency, many other dependencies will be installed on your machine, so called transitive dependencies. Any change in one of those dependencies can break your experiment. It's fundamental to have a way to state all the dependencies used, including the operating system, python interpreter and hardware that was used to run a certain experiment.

Dependency management is one of the most important requirements for reproducibility. Having dependencies clearly stated allows portability of notebooks, so they can be shared safely with others, reused in other projects or simply reproduced. If you want to know more about this issue in the data science domain, have a look at this [article](https://developers.redhat.com/blog/2021/03/19/managing-python-dependencies-with-the-thoth-jupyterlab-extension/) or this [video](https://www.youtube.com/watch?v=ifyQ2oSxjnU).

[Project Thoth][1] keeps dependencies up to date by giving recommendations through developer's daily tools. Thanks to this service, developers (including data scientists) do not have to worry about managing the dependencies after they are selected, since conflicts can be handled by Thoth bots and automated pipelines. Having this AI support can benefit AI projects, offering improvements such as performance improvements due to optimized dependencies and additional security since insecure libraries cannot be introduced. If you want to know more, have a look at [Thoth's website](https://thoth-station.ninja/docs/developers/adviser/integration.html).

Within the different Thoth integations, in this tutorial we are going to focus on the JupyterLab extension for dependency management, which is called [jupyterlab-requirements][2].

You can use this extension for each of your notebooks to guarantee they have the correct dependencies. This extension is able to add/remove dependencies, lock them and store them in the notebook metadata. In this way, all the dependencies information required to repeat the environment are shipped with the notebook.

In particular, the following notebook metadata is created for you, when you use Thoth's dependency management tool:

- `requirements` (Pipfile);

- `requirements locked` with all versions and hashes of libraries (direct and transitive ones) (Pipfile.lock);

- `dependency resolution engine` used (Thoth or Pipenv);

- `configuration file containing runtime environment` (only for Thoth resolution engine).

All this information can allow reproducibility and shareability of the notebook.


## What you will learn with this tutorial?

At the end of this tutorial you will be able to manage dependencies for your projects in Jupyter Notebooks, enabling others to reproduce what you did and allowing them to contribute to it. The last section will teach also how to enable [Kebechet Bot][5] to keep dependencies automatically up to date for you and how you can setup and use automatic pipelines from [AICoE CI][6] to create release and images of your projects that you can easily share with others.


## Where you will run this tutorial?

[Operate First][1] is an open infrastructure environment started at Red Hat's Office of the CTO. It has been selected to run this tutorial since it is an open source initiative that fulfills all the requirements stated above. Anyone with a Google account can log in and start developing. To learn more about Operate First, visit the [website](https://www.operate-first.cloud/) or [GitHub community](https://github.com/operate-first).

[Operate First][1] hosts [Open Data Hub][3] with all the tools provided for Data Science projects (e.g. JupyterHub, Elyra, Kubeflow Pipelines, Seldon, Prometheus, Grafana, Superset) running on [Red Hat Openshift][4].


## Why the tutorial repository has this structure?

The project template used can be found here: [project template][7]. It shows correlation between data scientist needs (e.g. data, notebooks, models) and AI DevOps engineers ones (e.g. manifests). Having structure in a project ensures all the pieces required for the ML and DevOps lifecycles are present and easily discoverable.


## Tutorial pre-requisites

0. [Pre-requisites](./docs/pre-requisite.md)

## Tutorial Steps

1. [Setup your initial environment](./docs/setup-initial-environment.md)

2. [Manage dependencies for your notebook](./docs/start-notebook-and-manage-dependencies.md)

3. [Push changes to GitHub](./docs/push-changes.md)

4. [Setup bots and pipelines to create releases, build images and enable automatic dependency management](./docs/thoth-aicoe-services.md)

5. [Share your work](./docs/share-your-work.md)


## References

* [Project Thoth][1]
* [jupyterlab-requirements][2]
* [Open Data Hub][3]
* [Red Hat Openshift][4]
* [Kebechet Bot][5]
* [AICoE CI][6]
* [project template][7]

[1]: https://thoth-station.ninja/
[2]: https://github.com/thoth-station/jupyterlab-requirements
[3]: https://opendatahub.io/
[4]: https://www.openshift.com/
[5]: https://github.com/marketplace/khebhut
[6]: https://github.com/AICoE/aicoe-ci
[7]: https://github.com/aicoe-aiops/project-template
