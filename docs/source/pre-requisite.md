# Pre-requisites

| pre-requisite | notes |
| ------------- | ------------------ |
| GitHub account | The project is based on GitHub, if you don't have one account, just follow this [link](https://docs.github.com/en/github/getting-started-with-github/signing-up-for-a-new-github-account). |
| GitHub token |  If you don't have a GitHub token, you can create one following GitHub docs: [create GitHub token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token). |
| [Red Hat Openshift][1] |  Using [Operate First][2] you can find a deployed [Red Hat Openshift][1] available to [Operate First][2] community. |
| [Open Data Hub][3] |  Using [Operate First][2] you can find a community supported [Open Data Hub][3] with all tools for Data Science (e.g. [JupyterHub][4], [Elyra][5], [Kubeflow Pipelines][6], [Seldon][7], [Prometheus][8], [Grafana][9], [Superset][10]) running on [Red Hat Openshift][1]. |
| JupyterLab environment with [jupyterlab-requirements][11] library and [Elyra][5] |  Using [Operate First][1], you can login in [JupyterHub][4] with your GitHub Account and you can spawn the image called [Experimental Elyra Notebook Image](https://github.com/operate-first/apps/blob/master/kfdefs/base/jupyterhub/notebook-images/experimental-elyra-notebook-imagestream.yaml), which has the library for dependency management already installed. If you use [Meteor][12], it will build a [JupyterHub][4] environment for your project from the GitHub repository URL you provide to it. (e.g. this [URL](https://github.com/pacospace/manage-dependencies-tutorial/)). |


## Next Step

[Setup your initial environment](./setup-initial-environment.md)


## References

* [Red Hat Openshift][1]
* [Operate First][2]
* [Open Data Hub][3]
* [JupyterHub][4]
* [Elyra][5]
* [Kubeflow Pipelines][6]
* [Seldon][7]
* [Prometheus][8]
* [Grafana][9]
* [Superset][10]
* [jupyterlab-requirements][11]
* [Meteor][12]

[1]: https://www.openshift.com/
[2]: https://www.operate-first.cloud/
[3]: https://opendatahub.io/
[4]: https://jupyter.org/hub
[5]: https://github.com/elyra-ai/elyra
[6]: https://www.kubeflow.org/docs/pipelines/overview/pipelines-overview/
[7]: https://www.seldon.io/
[8]: https://prometheus.io/
[9]: https://grafana.com/
[10]: https://superset.apache.org/
[11]: https://github.com/thoth-station/jupyterlab-requirements
[12]: https://github.com/AICoE/meteor
