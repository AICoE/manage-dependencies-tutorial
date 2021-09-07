# Create a first release and image of your project

This document describes how the [AICoE CI][1] and [Thoth](https://github.com/thoth-station) bots can be used to create the images for your project. If you want to build images and make release from your own fork, use the following instructions for image builds.


## Set up Thoth bots

Adding Thoth's bots takes just a few steps! 

### 1. Install Khebut

Start by installing the Kebechet GitHub application, called Khebut by [following this link](https://github.com/apps/khebhut). It can be configured on an organization or on a single repository.

Once the application is installed, you will need to add Thoth's bot (Sesheta) as collaborator. Navigate to the repo where you intalled Khebut. Under the repository's **Settings**, go to **Manage Access** and click on "Invite a collaborator" and add Thoth Bot Sesheta. Sesheta is a friendly Thoth bot who is used to help automate tasks. [Follow this link](https://github.com/AICoE/aicoe-ci/issues/new?assignees=goern%2Charshad16&labels=area%2Fcyborgs%2Cbot%2Csig%2Fcyborgs&template=request_sesheta.yaml&title=Help+with+Sesheta+invite) and fill out the form to have Sesheta accept your invitation. Please note: there is sometimes a delay in Sesheta's invite acceptance.

<div style="text-align:center">
<img alt="Invite Sesheta" src="https://raw.githubusercontent.com/aicoe/elyra-aidevsecops-tutorial/master/docs/images/InviteSesheta.png">
</div>

### 2. Enable issues on your fork

Sesheta, the bot that will assist you in this tutorial, communicates through issues. On your fork, the issues tab may not be enabled automatically. In order to enable issues, go to the **Settings** tab and check the box next to "Issues".

<div style="text-align:center">
<img alt="Enable Fork Issues" src="https://raw.githubusercontent.com/aicoe/elyra-aidevsecops-tutorial/master/docs/images/EnableForkIssues.png">
</div>

### 3. Add/Edit `.thoth.yaml`

Thoth services require a configuration file ([.thoth.yaml](../.thoth.yaml)) at the root level of the project. 

In this tutorial, the file is already present, so you will not need to add it. To configure this on your own fork, you will need to update the Kebechet [managers](https://github.com/thoth-station/kebechet/tree/master/kebechet/managers) section to include your GitHub username and push changes to your fork. Check [push changes section]((./push-changes.md)) for more details.

An example snippet of `.thoth.yaml` highlightling the changes to be made is shown below.

```yaml
host: khemenu.thoth-station.ninja
tls_verify: false
requirements_format: pipenv

runtime_environments:
  - name: tutorial  # runtime environment name
    operating_system:
      name: rhel
      version: "8"
    python_version: "3.8"
    recommendation_type: latest

managers:
  - name: pipfile-requirements
  - name: update
    configuration:
      labels: [bot]
  - name: info
  - name: version
    configuration:
      maintainers:
        - pacospace # UPDATE TO HAVE YOUR OWN USERNAME
      assignees:
        - sesheta
      labels: [bot]
      changelog_file: true
```

To learn more about Thoth bots and services, please check out the guide [here][2].

NOTE: _If you obtained the dependencies locked using Thoth dependency resolution engine, `.thoth.yaml` used is stored in the notebook metadata. You can extract it and place it at the root of the repo, simply running: `%horus extract --thoth-config --store-files-path <PATH_TO_STORE>`._


## Set up AICoE CI

The [AICoE-CI tooling](https://github.com/AICoE/aicoe-ci) can be set up in just a few steps.

### 1. Install AICOE CI

Start by installing the AICoE CI GitHub application by [following this link](https://github.com/apps/aicoe-ci). When installing this application, select your profile for the organization, and specify the repository you are working on.

### 2. Set up robot account

This step is required to create credentials for the aicoe-ci to push to your container registry (e.g. Quay).

#### Quay

These steps are specific for users with Quay account and they will involve setting up a robot account on the image registry [Quay.io](https://quay.io/).

First, you will need to create a robot in the organization or individual account. Under **Account Settings** on Quay, click on **Robot Accounts** tab, and "Create Robot Account" button. Enter a name for the account. The username will become namespace+accountname where namespace is the name of the user or organization.

<div style="text-align:center">
<img alt="Create Robot Account" src="https://raw.githubusercontent.com/AICoE/aicoe-ci/master/docs/quay-robots.png">
</div>

Once created, click on the robot account name. Find the "Docker Configuration" tab in the robot account popup, and copy the .json. Currently, you will have to pass it on by contacting us. You can reach us at `aicoe-thoth+devconf@redhat.com`. Once the secret is passed, it is ready to be used in the `.aicoe-ci.yaml` file in the next step.

## 3. Edit `.aicoe-ci.yaml`

The last step is to add the [aicoe-ci configuration file](https://github.com/AICoE/aicoe-ci#aicoe-ci-configuration-file). Configuration files allows user assign details about the build requirements and specify base image and registry details for build and push. For the purpose of this tutorial, the [.aicoe-ci.yaml](../.aicoe-ci.yaml) file is already present. However, you may need to edit some of the fields for your personal access, namely `registry-org`, `registry-project`, and `registry-secret`.

```yaml
check:
  - [] # Enable checks for your repo (pre-commit, build, pytest)
build:
  base-image: "quay.io/thoth-station/s2i-elyra-custom-notebook:v0.3.3"
  build-source-script: "image:///opt/app-root/builder"
  custom-tag: latest
  build-stratergy: Source # Allowed values: Source, Dockerfile, Containerfile
  registry: quay.io # Image registry to be used. (default: quay.io)
  registry-org: thoth-station # Organization in Image Registry. (default: thoth-station)
  registry-project: manage-dependencies-tutorial # project repository in Image Registry (ie, Quay) used to push image.
  registry-secret: thoth-station-thoth-pusher-secret # comes from robot account
```

For more detailed information on the config file and robot accounts, visit the [AICoE CI documentation](https://github.com/AICoE/aicoe-ci#configuring-build-requirements).
Once you modify the `.aicoe.yaml` push the changes to your repo. Check [push changes section]((./push-changes.md)) for more details.


## Get new release

Some of the pipelines used in the Thoth project are maintained by bots. Therefore you can simply open an issue asking for a release (e.g patch, minor, major) and the bots will handle your request. Once the request is completed, the bot will also automatically close the issue, as you can see from the images below:

<div style="text-align:center">
<img alt="Open Issue Release" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/OpenIssueRelease.png">
</div>

<div style="text-align:center">
<img alt="Pull Request Release" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/PullRequestRelease.png">
</div>

Fun fact, the `CHANGELOG` in the release is also created using an AI model that clusters pull requests. You can find more information about this model in our [glyph][3] project.

Once the issue is closed by the bot, a new tag is created in the GitHub repo. This in turn triggers the Tekton pipelines in AICoE CI to start the build process and push the image on the registry according to the configuration defined in the [.aicoe-ci.yaml](../.aicoe-ci.yaml).

Once the image has been created by the Tekton pipelines, you can find it in your registry (e.g. Quay):

<div style="text-align:center">
<img alt="Image on Registry" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/ImageRegistry.png">
</div>

## Dependencies updates in the repo

Once you install Khebut in your repo, you can benefit from different [services](https://github.com/thoth-station/kebechet#kebechet) just setting correctly the `.thoth.yaml` configuration file.

Thoth bots regularly checks if your project is using the optimal set of dependencies in terms of CVE vulnerabilities, newer package releases, and performance changes. If it finds that the dependencies can be updated, it automatically opens a PR on your repo to make the required updates!

An example of the Khebut bot in action can be seen below.

<div style="text-align:center">
<img alt="Khebut Automatic Update" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/KhebutAutomaticUpdate.png">
</div>


## End of tutorial

Now you are ready to continue working on your project safely, creating releases and having dependencies maintained by bots. Your repo now also satisfies the requirements to use project [Meteor](https://github.com/AICoE/meteor) directly from [Operate First](https://www.operate-first.cloud/). Check this [link](http://meteor-shower-aicoe-meteor.apps.zero.massopen.cloud/).

## References

* [AICoE CI Pipeline][1]
* [Setting AICoE CI on a GitHub repo/org][2]
* [Project Glyph][3]
* [Kebechet][4]
* [Bots and CI Services Setup Instructions][5]

[1]: https://github.com/AICoE/aicoe-ci
[2]: https://github.com/AICoE/aicoe-ci#setting-aicoe-ci-on-github-organizationrepository
[3]: https://github.com/thoth-station/glyph
[4]: https://github.com/thoth-station/kebechet
[5]: https://github.com/AICoE/aicoe-ci/blob/master/docs/thoth-bots-setup.md#instructions-to-setup-bots-and-ci-services
