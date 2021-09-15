# Create a first release and image of your project

This section describes how the [AICoE CI][1] and [Thoth](https://github.com/thoth-station) bots can be used to maintain dependencies and create the images for your project.

In particular:

- [AICoE CI][1] is Continuous integration system used for running status checks on pull request, build releases, and python module releases.

- [Kebechet Bot][4] is used to keep your dependencies fresh and up to date receiving recommendations and justifications using AI (Thoth service).

These bots and pipelines exist to automate many of the manual GitOps tasks (e.g. in order to deploy your application, you may need to create a container image). [GitHub templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates) integrated with bots can provide you with automated pipelines triggered depending on what you need (e.g. release (patch, minor, major), deliver a container image, or update your dependencies).

The next steps will teach you how to install and enable those tools and trigger them.


## Set up Thoth bots

Adding Thoth's bots takes just a few steps!

### 1. Install Khebut

Start by installing the Kebechet GitHub application, called Khebut by [following this link](https://github.com/apps/khebhut). It can be configured on an organization or on a single repository.

Once the application is installed, you will need to add Thoth's bot (Sesheta) as collaborator. Navigate to the repo where you intalled Khebut. Under the repository's **Settings**, go to **Manage Access** and click on "Invite a collaborator" and add Thoth Bot Sesheta. Sesheta is a friendly Thoth bot who is used to help automate tasks. [Follow this link](https://github.com/AICoE/aicoe-ci/issues/new?assignees=goern%2Charshad16&labels=area%2Fcyborgs%2Cbot%2Csig%2Fcyborgs&template=request_sesheta.yaml&title=Help+with+Sesheta+invite) and fill out the form to have Sesheta accept your invitation. Please note: there is sometimes a delay in Sesheta's invite acceptance.

<div style="text-align:center">
<img alt="Invite Sesheta" src="https://raw.githubusercontent.com/aicoe/elyra-aidevsecops-tutorial/master/docs/images/SeshetaInvite.png">
</div>

### 2. Enable issues on your fork

Sesheta, the bot that will assist you in this tutorial, communicates through issues. On your fork, the issues tab may not be enabled automatically. In order to enable issues, go to the **Settings** tab and check the box next to "Issues".

<div style="text-align:center">
<img alt="Enable Fork Issues" src="https://raw.githubusercontent.com/aicoe/elyra-aidevsecops-tutorial/master/docs/images/SeshetaEnableForkIssues.png">
</div>

### 3. Edit `.thoth.yaml`

Thoth services require a configuration file ([.thoth.yaml](../.thoth.yaml)) at the root level of the project. This tutorial is based on [project-template][8], therefore the .thoth.yaml is already present.

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

### 4. Push changes to GitHub

Once you modify the `.thoth.yaml` push the changes to your repo. Check [push changes section]((./push-changes.md)) for more details.


## Set up AICoE CI

The [AICoE CI][1](https://github.com/AICoE/aicoe-ci) can be set up in just a few steps.

### 1. Install AICOE CI

Start by installing the AICoE CI GitHub application by [following this link](https://github.com/apps/aicoe-ci). When installing this application, select your profile for the organization, and specify the repository you are working on (e.g. `manage-dependencies-tutorial`).

### 2. Set up robot account

This step is required to create credentials for the aicoe-ci to push to your container registry (e.g. Quay).

#### Quay

These steps are specific for users with Quay account and they will involve setting up a robot account on the image registry [Quay.io](https://quay.io/).

First, you will need to create a robot in the organization or individual account. Under **Account Settings** on Quay, click on **Robot Accounts** tab, and "Create Robot Account" button. Enter a name for the account. The username will become namespace+accountname where namespace is the name of the user or organization.

<div style="text-align:center">
<img alt="Create Robot Account" src="https://raw.githubusercontent.com/AICoE/aicoe-ci/master/docs/quay-robots.png">
</div>

Once created, click on the robot account name. Find the "Docker Configuration" tab in the robot account popup, and copy the .json. Currently, you will have to pass it on by contacting us. You can reach us at `aicoe-thoth+devconf@redhat.com`. Once the secret is passed, it is ready to be used in the `.aicoe-ci.yaml` file in the next step.

### 3. Login into your container registry and create new repository

Click on `+ Create New Repository` button on the upper left part:

<div style="text-align:center">
<img alt="Create New Repository" src="https://raw.githubusercontent.com/aicoe/elyra-aidevsecops-tutorial/master/docs/images/QuayCreateNewRepository.png">
</div>


### 4. Add the name of the repository and make it public

<div style="text-align:center">
<img alt="Create Public Quay repository" src="https://raw.githubusercontent.com/aicoe/elyra-aidevsecops-tutorial/master/docs/images/QuaySetPublicRepository.png">
</div>


### 5. Set robot permissions for your repo

1. Once the repository is created, go to `Setting`:

<div style="text-align:center">
<img alt="Go to Setting for your Repo" src="https://raw.githubusercontent.com/aicoe/elyra-aidevsecops-tutorial/master/docs/images/QuayRepositorySettings.png">
</div>

2. Under `User and Robot Permissions` you can add the Robot Account created at point 2:

<div style="text-align:center">
<img alt="Set Robot Account to your Repo" src="https://raw.githubusercontent.com/aicoe/elyra-aidevsecops-tutorial/master/docs/images/QuaySetRobotAccountRepository.png">
</div>

3. Set Robot Permission to `Write`:

<div style="text-align:center">
<img alt="Set Robot Permission to Write to your Repo" src="https://raw.githubusercontent.com/aicoe/elyra-aidevsecops-tutorial/master/docs/images/QuaySetRobotPermissionsWriteRepository.png">
</div>

4. Click `Add Permission`:

<div style="text-align:center">
<img alt="Add Permission for the Robot Account" src="https://raw.githubusercontent.com/aicoe/elyra-aidevsecops-tutorial/master/docs/images/QuayAddRobotPermissionsRepository.png">
</div>

Now everything is set on your container registry and the AICoE-CI will be able to push to your container image in your registry. Last step will be configuring the AICOE-CI to know where to push.

### 6. Edit `.aicoe-ci.yaml`

The last step is to edit the [aicoe-ci configuration file](https://github.com/AICoE/aicoe-ci#aicoe-ci-configuration-file). This tutorial is based on [project-template][8], therefore the .thoth.yaml is already present. The `.aicoe.yaml` onfiguration file allows user to assign details about the build requirements and specify base image and registry details for build and push. For the purpose of this tutorial, the [.aicoe-ci.yaml](../.aicoe-ci.yaml) file is already present. However, you may need to edit some of the fields for your personal access, namely `registry-org`, `registry-project`, and `registry-secret`.

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
  registry-project: manage-dependencies-tutorial # project repository in Image Registry (ie, Quay) used to push image (created in point 3.).
  registry-secret: thoth-station-thoth-pusher-secret # comes from robot account (created in point 2.)
```

For more detailed information on the config file and robot accounts, visit the [AICoE CI documentation](https://github.com/AICoE/aicoe-ci#configuring-build-requirements).

### 7. Push changes to GitHub

Once you modify the `.aicoe.yaml` push the changes to your repo. Check [push changes section]((./push-changes.md)) for more details.


## Create new release

Now that everything is set you can create new images. Some of the pipelines used in the Thoth project are maintained by bots. Therefore you can simply open an issue asking for a release (e.g patch, minor, major) and the bots will handle your request. Once the request is completed, the bot will also automatically close the issue, as you can see from the images below:

<div style="text-align:center">
<img alt="Open Issue Release" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/KhebutOpenIssueRelease.png">
</div>

<div style="text-align:center">
<img alt="Pull Request Release" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/KhebutPullRequestRelease.png">
</div>

Fun fact, the `CHANGELOG` in the release is also created using an AI model that clusters pull requests. You can find more information about this model in our [glyph][3] project.

Once the issue is closed by the bot, a new tag is created in the GitHub repo. This in turn triggers the Tekton pipelines in AICoE CI to start the build process and push the image on the registry according to the configuration defined in the [.aicoe-ci.yaml](../.aicoe-ci.yaml).

Once the image has been created by the Tekton pipelines, you can find it in your registry (e.g. Quay):

<div style="text-align:center">
<img alt="Image on Registry" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/QuayImageRegistry.png">
</div>

## Dependencies updates in the repo

Once you install Khebut in your repo, you can benefit from different [services](https://github.com/thoth-station/kebechet#kebechet) just setting correctly the `.thoth.yaml` configuration file.

Thoth bots regularly checks if your project is using the optimal set of dependencies in terms of CVE vulnerabilities, newer package releases, and performance changes. If it finds that the dependencies can be updated, it automatically opens a PR on your repo to make the required updates!

An example of the Khebut bot in action can be seen below.

<div style="text-align:center">
<img alt="Khebut Automatic Update" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/KhebutAutomaticUpdate.png">
</div>


## Next Step

[Share your work](./share-your-work.md)


## References

* [AICoE CI][1]
* [Setting AICoE CI on a GitHub repo/org][2]
* [Project Glyph][3]
* [Kebechet Bot][4]
* [Bots and CI Services Setup Instructions][5]
* [Project Meteor][6]
* [Operate First][7]
* [project-template][8]

[1]: https://github.com/AICoE/aicoe-ci
[2]: https://github.com/AICoE/aicoe-ci#setting-aicoe-ci-on-github-organizationrepository
[3]: https://github.com/thoth-station/glyph
[4]: https://github.com/thoth-station/kebechet
[5]: https://github.com/AICoE/aicoe-ci/blob/master/docs/thoth-bots-setup.md#instructions-to-setup-bots-and-ci-services
[6]: https://github.com/AICoE/meteor
[7]: https://www.operate-first.cloud/
[8]: https://github.com/aicoe-aiops/project-template
