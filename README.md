# Thoth Tutorial - manage your dependencies in Jupyter notebooks.

This tutorial is used to show how to manage dependencies for Jupyter Notebooks to allow reproducibility and shareability. In this way you learn how to move from local machine to cloud, running on [Operate First][1], and how you can enable contributions on your project from other team members.

Once the tutorial is completed, you will be able to run your work on [Project Meteor][2].

## Environment and Tools

In this tutorial the following technologies are going to be used:

- [jupyterlab-requirements][3] library. ([Project Thoth][4], JupyterLab extension for dependency management)
- [JupyterHub][5] to launch images with Jupyter tooling.

If you use the [Operate First][1] environment, the above requirements will be already setup for you selecting `elyra-image` from [JupyterHub][5].

### Operate First Open Environment

[Operate First][1] is an open infrastructure environment started at Red Hat's Office of the CTO. It has been selected to run this tutorial since it is an open source initiative that fulfills all the requirements stated above. Anyone with a Google account can log in and start developing. To learn more about Operate First, visit the [website](https://www.operate-first.cloud/) or [GitHub community](https://github.com/operate-first).


## Project templates

The tutorial structure follows this [project template][6]. Having structure in a project ensures all the pieces required for the project lifecycle are present and easily discoverable.

If you want to use this template for your AI project, go to this [project template][6] and click the `Use the template` button provided in the repository for your new projects.

<div style="text-align:center">
<img alt="AI Project Template" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/AIProjectTemplate.png">
</div>


## Automated pipelines and bots for your GitHub project

- [Kebechet Bot][7] to keep your dependencies fresh and up to date receiving recommendations and justifications using AI.

- [AICoE CI][8] to support your AI project lifecycle.

All these tools are integrated with the [project template][6], so most additions are already set for you.
These bots and pipelines exist to automate many of the manual GitOps tasks. For example, in order to deploy your application, you may need to create a container image. GitHub templates integrated with bots can provide you with automated pipelines triggered depending on what you need (e.g. release (patch, minor, major), deliver a container image, or update your dependencies).


## GitOps for reproducibility, portability, traceability with AI support

Nowadays, developers (including data scientists) use Git and GitOps practices to store and share code on development platforms such as GitHub. GitOps best practices allow for reproducibility and traceability in projects.

One of the most important requirements for reproducibility is dependency management. Having dependencies clearly stated allows portability of notebooks, so they can be shared safely with others and reused in other projects.

If you want to know more about this issue in the data science domain, have a look at this [article](https://developers.redhat.com/blog/2021/03/19/managing-python-dependencies-with-the-thoth-jupyterlab-extension/) or this [video](https://www.youtube.com/watch?v=ifyQ2oSxjnU).

[Project Thoth][4] keeps dependencies up to date by giving recommendations through developer's daily tools. Thanks to this service, developers (including data scientists) do not have to worry about managing the dependencies after they are selected, since conflicts can be handled by Thoth bots and automated pipelines. Having this AI support can benefit AI projects, offering improvements such as performance improvements due to optimized dependencies and additional security since insecure libraries cannot be introduced. If you want to know more, have a look at this [repo](https://github.com/thoth-station/jupyterlab-requirements) or Thoth's [website](https://thoth-station.ninja/docs/developers/adviser/integration.html).


## Tutorial pre-requisites

0. [Pre-requisites](./docs/pre-requisite.md)

## Tutorial Steps

1. [Setup your initial environment](./docs/setup-initial-environment.md)

2. [Manage dependencies for your notebook](./docs/start-notebook-and-manage-dependencies.md)

3. [Push changes to GitHub](./docs/source/push-changes.md)

4. [Setup bots and pipelines to create releases, build images and enable automatic dependency management](./docs/thoth-aicoe-services.md)


## References

* [Operate First][1]
* [Project Meteor][2]
* [jupyterlab-requirements][3]
* [Project Thoth][4]
* [JupyterHub][5]
* [project-template][6]
* [Kebechet Bot][7]
* [AICoE CI][8]

[1]: https://www.operate-first.cloud/
[2]: https://github.com/AICoE/meteor
[3]: https://github.com/thoth-station/jupyterlab-requirements
[4]: https://jupyter.org/hub
[5]: https://thoth-station.ninja/
[6]: https://github.com/aicoe-aiops/project-template
[7]: https://github.com/marketplace/khebhut
[8]: https://github.com/AICoE/aicoe-ci
