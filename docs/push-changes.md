# Push your changes on your GitHub repo

If you don't have a GitHub token, you can create one following GitHub docs: [create GitHub token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token).

## Push your changes using JupyterLab Git extension

If you are running this tutorial on Operate First your work-in-progress notebooks can be saved in your JupyterHub PVC by hitting the save button on the top panel.
Nevertheless, it is a good practice to push your changes to the GitHub repo when you finish working on your project, so that all your work can be saved.

In order to do that from within JupyterHub using the [Jupyterlab Git extension](https://github.com/jupyterlab/jupyterlab-git):

1. Go to Git Box panel on the left to check what files have been changed.

    <div style="text-align:center">
    <img alt="Go to Git Box Panel" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabGitBoxPanel.png">
    </div>

2. Stage the files you want to push to your GitHub repo.

    <div style="text-align:center">
    <img alt="Stage the files" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabGitStageFiles.png">
    </div>

3. Add Summary of your changes (a.k.a commit message) and select Commit.

    <div style="text-align:center">
    <img alt="Commit Changes" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabGitCommitChanges.png">
    </div>

    NOTE: _If you are doing this for the first time, git requires user email and user name to be set.(The extension will open a Dialog Form to insert them)_

    <div style="text-align:center">
    <img alt="Insert User Name and Email" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabGitInsertUserNameEmail.png">
    </div>


4. Select Push Changes.

    <div style="text-align:center">
    <img alt="Use Button to Push Changes" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabGitUseButtonToPushChanges.png">
    </div>

5. Insert your Github account name and your GitHub token to push to the GitHub repo you cloned.

    <div style="text-align:center">
    <img alt="Push Changes with GitHub token" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabGitPush.png">
    </div>

## Push your changes using the terminal in JupyterLab

If you want to clone a repo and push changes through the Terminal, you can use the following steps.

1. Open terminal from the icon in the Launcher.

    <div style="text-align:center">
    <img alt="Open Terminal" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabOpenTerminal.png">
    </div>

2. Start using the git commands:

    <div style="text-align:center">
    <img alt="Use Git Commands" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabUseTerminal.png">
    </div>

- `git clone <repo>` to clone a new repo.

- `git add <file>` after you modify files to put them in stage.

- `git commit -m "<commit message>"` to commit the changes in stage. _NOTE: If you are doing this for the first time, git requires user email and user name to be set._

    <div style="text-align:center">
    <img alt="First commit" src="https://raw.githubusercontent.com/AICoE/manage-dependencies-tutorial/master/docs/images/JupyterLabTerminalFirstCommit.png">
    </div>

- `git push origin <branch>` to push your changes.


## Next Step

[Set bots and pipelines to create releases, build images and enable dependency management](./thoth-aicoe-services.md)
