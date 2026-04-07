<!-- Development > Projects > Versioning of server project content -->

## 13. Versioning of server project content

This section describes the most basic use cases of versioning server projects with two popular version control systems. It describes the way to use the particular version system and **CloverDX Designer** together. It does not serve to replace the documentation of any particular version control system.

We encourage you to read the documentation for version control system tool of your choice as well.

Server projects store files remotely and locally. This allows you to use **version control system** of your choice. You can use an Eclipse plugin as well as an external tool. The basic workflow of usage of Git and SVN versioning systems in **CloverDX Designer** is described below.

### Version sontrol system files and synchronization

Version control system metadata files (e.g .svn directory) *must not* be synchronized between **Designer** and **Server**. These files avoided from synchronization are listed in **Preferences** under [Ignored files](../admin/designer-configuration.md#ignored-files) section. If you use **Bazaar**, **Git**, **Mercurial**, or **SVN**, you do not have to care about this, as it is already configured. If you use any other version control system, you should add its files and directories to this list of ignored files.

### Versioning tools

The following text describes the basic work flows with Git and SVN. For both, an approach with an Eclipse plugin (EGit, Subclipse), external GUI tool (TortoiseGit, TortoiseSVN) and command line utilities is described.

**EGit** is an Eclipse plugin for versioning with Git. It is included in **CloverDX Designer**.

**Subclipse** is an Eclipse plugin for versioning with SVN. Since it is not part of **CloverDX Designer**, you need to install it, e.g from **Eclipse Marketplace**.

**TortoiseGit** and **TortoiseSVN** are external GUI tools.

### Initial check-out of project from repository

| [GIT](server-projects-versioning.md#git) |
| --- |
| [SVN](server-projects-versioning.md#svn) |

There is an existing project in the repository. Your task is to create a new server project with content from the repository.

#### GIT

| [Eclipse plugin - EGit](server-projects-versioning.md#eclipse-plugin-egit) |
| --- |
| [External GUI tool - TortoiseGit](server-projects-versioning.md#external-gui-tool-tortoisegit) |
| [External Command line tool](server-projects-versioning.md#external-command-line-tool) |

To version files with Git, you can use Eclipse plugin (**EGit**), external GUI or command line tool.

##### Eclipse plugin - EGit

1. Clone the remote Git repository:
   Switch to **Git** perspective.
   In the **Git Repositories** tab, click **Clone a Git Repository and add the clone to this view**.
   Enter the remote repository location and password.
   Choose branches to be tracked.
   Enter the path for the local repository.
   Switch back to **CloverDX** perspective.
2. Import the project.
   From the **File** menu, choose **Import**.
   Choose **Git** ****Projects from Git** and click **Next**.
   Choose **Existing local repository**.
   Choose the repository.
   Select the **Import existing projects** option.
   Select projects that should be imported.
3. Convert the project to **server project**.
   Right click the project in **Project Explorer** and choose **Convert to server project.**
   Enter **CloverDX Server URL**, **User** name and **Password**.
   Select **Create new sandbox**. Enter the sandbox **Name**.
   Select type of merge. As you created a new sandbox, you can use the **Use local content only (sandbox will be cleaned)** option.

You have a new server project. The project has content of a master branch of local repository.

**EGit** allows you to have more projects within the same repository.

##### External GUI tool - TortoiseGit

1. Clone the remote repository.
   In **File Explorer**, right click and choose **Git Clone**.
   In **Git clone - TortoiseGit** dialog, enter the path to remote repository and the path to local repository.
   Click **OK**.
   Enter password.
   Close the cloning log window.
2. Import the project.
3. Convert project to **server project**.

##### External Command line tool

1. Clone the git repository
   Type the command
   ```bash
   git clone path_to_remote path_to_local
   ```
   e. g.
   ```bash
   git clone ssh://git@127.0.0.1:30022/home/git/project1 project1
   ```
2. Import the project.
3. Convert project to **server project**.

#### SVN

| [Eclipse plugin - Subclipse](server-projects-versioning.md#eclipse-plugin-subclipse) |
| --- |
| [External GUI tools - TortoiseSVN](server-projects-versioning.md#external-gui-tools-tortoisesvn) |
| [Command line tools](server-projects-versioning.md#command-line-tools) |

##### Eclipse plugin - Subclipse

1. Import project from SVN.
   Choose **File** ****Import**.
   Choose **SVN** ****Checkout Projects from SVN**.
   In **Select/Create Location** step of the wizard, choose **Create new repository location**.
   Specify location of SVN repository. The URL for remote projects can be, e.g. `https://svn.example.org/svn`. The URL for local projects can be, e.g. `file:///Users/clover/repositories/svn/repo1`.
   Select the folder (project) to be imported.
   In **Check Out As** step, choose **Check out as a project in the workspace** and change **ProjectName** if necessary.
   Optionally, change the location to which the project will be checked or add the project to working sets.
2. Convert the project to **server project**.

##### External GUI tools - TortoiseSVN

You can use an external graphical tool to check out an svn project. The following steps describe checking out of an existing project with help of **TortoiseSVN**.

1. Check-out the content of projects from SVN:
   Right click the project directory in File Explorer and choose **SVN Checkout…​** from context menu.
   Delete the last entry from the **Checkout directory** text field. Click **OK**.
   **TortoiseSVN** complains that the directory is not empty. Choose **Yes**.
2. Import the project.
3. Convert the project to **server project**.

##### Command line tools

1. Check out the project from svn:
   Move to the directory with the Project in workspace (on the computer with Designer).
   Type `svn checkout --force /path/to/repository .` The `--force` forces `svn` to overwrite the content created during the project creation. Otherwise, you would have to resolve conflicts after checkout.
2. Import the project.
3. Convert the project to **server project**.

### Adding server project to version control

| [Git](server-projects-versioning.md#git) |
| --- |
| [SVN](server-projects-versioning.md#svn) |

This section describes a way to create a brand new versioned server project and to commit it to a new remote repository. It describes the way to add an existing unversioned server project to the repository as well.

Generally, create a new server project, then add it under a version control system.

#### Git

| [Eclipse plugin - Egit](server-projects-versioning.md#eclipse-plugin-egit) |
| --- |
| [External GUI tool - TortoiseGit](server-projects-versioning.md#external-gui-tool-tortoisegit) |
| [External tool - Command line](server-projects-versioning.md#external-tool-command-line) |

**EGit** does not place the `.git` directory into the project directory. It creates the local Git repository outside the project, creates a project directory within the repository, and links the project directory into the workspace.

##### Eclipse plugin - Egit

1. Create a new local repository.
   Open a new perspective.
   Choose **Git**.
   In **Git Repositories** tab, click the **Create a new Git Repository and add it to this view** icon.
   In **Create a Git Repository** dialog, enter the path to the local Git repository.
   Switch back to **CloverDX Perspective**.
2. Create a new server project.
3. Share the project with **Team → Share** wizard:
   Right click the project name in the **Project Explorer** and choose **Team** ****Share Project…​**.
   In the **Share Project** wizard, choose **Git**.
   Create a new Git repository: click the **Create…​** button in the upper right corner and choose new repository location.
   If you intend to store more projects within one repository, enter **Path within repository**.
   You usually do not check the **Use or create repository in parent folder of project** checkbox.
   Click **Finish**.
   The Git share wizard will move you project to the local Git repository and *link* the project to your workspace.
4. Optionally, ignore the files or directories that you would not like to commit into repository: right click the file in **Project Explorer** and choose **Team** ****Ignore**.
5. Commit the changes into the local repository:
   Right click the project in **Project Explorer** and choose **Team** ****Commit**.
   Choose files, type the commit message, and click **Commit**.
6. Push the changes into to the remote repository:
   Switch to the **Git** perspective.
   Unfold the **Project**.
   Right click **Remotes** and choose **Create Remotes…​**.
   Enter the name for remote repository. Usually, it is called *origin*.
   In the second step of the wizard, click **Change** to specify the URI of remote repository. Enter URI and password and click **Finish**.
   Click **Advanced** to specify tracking of remote branches. Choose branches below the **Source ref** and **Destination ref** titles. Click **Add spec** to add the tuple to the list of tracked branches.
   Tick **Save specifications in 'remote' configuration**. Click **Finish** to close **Configure Push** dialog.
   Click **Save and Push** to save the branch tracking and to push the changes from local repository to remote one.

##### External GUI tool - TortoiseGit

1. Create a new local repository.
   Create a new directory for repository.
   Right click this directory in the **File Explorer** and choose **Git Create repository here …​** from the context menu.
   Do not make it *bare*.
2. Create a new server project. In the last step of the wizard, uncheck **Use default location** and enter the path to the local repository.
3. Make initial commit.
   Right click the project directory and choose **Git commit → "master" …​** from the context menu.
   In the **commit dialog**, right click the files that you do not want to version and choose **Add to ignore list** ****"the file name"**. In **ignore** dialog, use defaults.
   Select all files in repository, type commit message and click **commit**.
4. Configure the tracking of remote repository and push the local commit.
   In **File Explorer**, right click the project and choose **TortoiseGit** ****Push**.
   In **TortoiseGit - Push** dialog, click **Manage**.
   In **Settings - TortoiseGit**, enter **URL** or remote repository and click **OK**.
   Click **OK** to push the changes to remote repository.
   Type the password and close the log.

##### External tool - Command line

1. Create a new local Git repository.
   Type `git init /path/to/repository`
2. Create a new server project. In the last step of the wizard, uncheck **Use default location** and enter the path to the local repository.
3. Optionally, add a list of files or directories that should not be versioned to `.gitignore`
   `echo file_name >> .gitignore`
4. Commit the changes to local repository.
   `git commit -a -m "Initial commit"`
5. Add remote repository.
   `git remote add origin ssh://git@127.0.0.1:30022/home/git/repos/Project.git`
6. Push the commits to remote repository.
   `git push --set-upstream origin master`

#### SVN

| [Eclipse plugin - Subclipse](server-projects-versioning.md#eclipse-plugin-subclipse) |
| --- |
| [External tool - TortoiseSVN](server-projects-versioning.md#external-tool-tortoisesvn) |
| [External tool - Command line](server-projects-versioning.md#external-tool-command-line) |

##### Eclipse plugin - Subclipse

1. Create a new (Synchronized) server project. See [CloverDX server project](first-cloverdx-project.md#cloverdx-server-project).
2. Share the project with **Team → Share** wizard.
   Right click in **Project Explorer** and choose **Team** ****Share Project…​** from the context menu.
   In the **Share project** wizard, choose **SVN**.
   Choose **Use existing repository location**.
   Enter folder name. Click **Next**.
   Type the **Commit message**. Click **Finish**.
   The root directory of your project has been committed.
3. Optionally, add a list of files or directories that should not be versioned to `svn:ignore`:
   In **Project Explorer** in **CloverDX Perspective**, right click the file or directory and select **Team** ****Add to svn:ignore…​**.

The project has been created and the root directory has been committed into the repository.

You might need to commit the files and directories as well. See [Committing into Repository](server-projects-versioning.md#committing-into-repository).

##### External tool - TortoiseSVN

**TortoiseSVN** does not let you choose particular files during the import into repository. Therefore you should create a project directory and import repository first. Then you can set up list of files or directories that should not be committed.

1. Create a project directory.
2. Commit the directory to repository:
   Right click the directory and choose **TortoiseSVN** ****Import**.
   In the dialog, enter the URL of repository and the commit message. Generally, the URL has a format: `somePath/MyProjectName`.
3. Check out the repository.
   In **FileExplorer** choose the project directory and choose **SVN Checkout…​**
4. Create a new (Synchronized) server project. See [CloverDX server project](first-cloverdx-project.md#cloverdx-server-project).
5. Avoid committing of files or directories that should not be committed.
   In **File Explorer**, right click the file or directory within the project and choose **TortoiseSVN** ****Add to ignore list** ****"the file name"**
6. Commit the project:
   In **File Explorer**, right click the project name and choose **SVN Commit…​**

##### External tool - Command line

1. Create a project directory.
   `mkdir MyProject`
2. Import the directory to repository.
   `svn import MyProject url_to_repository -m "Initial import"`
3. Check out the committed directory. It converts the project directory into a working copy.
   `svn co url_to_repository/MyProject MyProject`
4. Create a new server project.
5. Optionally, add files or directories to `svn:ignore`.
   Move to the project and type `svn propset svn:ignore file_name`.
6. Add files and commit the changes.
   svn add *
   svn commit -m "Initial import"

### Connecting server project to existing repository

| [Git](server-projects-versioning.md#git) |
| --- |
| [SVN](server-projects-versioning.md#svn) |

There is an existing Server sandbox with some data, graphs, jobflows, etc. The content of the sandbox is in repository as well.

This section describes a way to create a new server project corresponding to this sandbox and to attach the project with versioning system.

#### Git

Cloning the remote repository and binding the content of an existing sandbox with the project from this repository is almost same as [Initial Check-Out of Project from Repository](server-projects-versioning.md#initial-check-out-of-project-from-repository).

The difference is that in the second step of the **New server project** wizard you should choose an existing sandbox.

#### Eclipse plugin - EGit

1. Clone the repository.
   Switch to **Git** perspective.
   In **Git Repositories** tab, click the **Clone a Git Repository and add the clone to this view** icon.
   Enter the remote repository location and password.
   Choose branches to be tracked.
   Enter the location at which the local repository will be created.
   Switch back to **CloverDX** perspective.
2. Import the project from the local Git repository.
3. Convert the project to **server project**.
   In the second step of wizard, choose an existing server sandbox.
   In the last step of the wizard, choose the type of merge, e.g. **Merge content - prefer remote files**.

#### External lool - TortoiseGit

1. Clone the git repository.
2. Import the project.
3. Convert project to **server project**.

#### External tool - Command line

1. Clone the Git repository.
   `git clone /path/to/remote/repo local_repo`
2. Import the project.
3. Convert the project to **server project**.

#### SVN

##### Eclipse plugin - Subclipse

1. Checkout the project from SVN.
2. Import the project.
3. Convert the project to **server project**.

##### External tool - TortoiseSVN

1. Check out the repository to directory with project.
   Right click the project directory in **File Explorer** and choose **SVN Checkout…​**
   Specify the checkout directory as current directory and click **OK**.
   **TortoiseSVN** complains that the directory is not empty.
2. Import the project.
3. Convert project to **server project**.

##### External tool - Command line

1. Check out the project from SVN.
   `svn checkout --force /path/to/repository`
2. Import the project.
3. Convert the project to **server project**.

### Getting changes from repository

| [Git](server-projects-versioning.md#git) |
| --- |
| [SVN](server-projects-versioning.md#svn) |

You have a server project connected to a repository. This section describes a way to get changes made by your colleagues from the repository.

#### Git

In Git terminology, this process is known as *git pull*. Instead of *pull*, you can do *fetch* and *merge*, or *fetch* and *rebase*.

##### Eclipse plugin - EGit

In **Project Explorer**, right click the project and choose **Team** ****Pull**

##### External tool - TortoiseGit

1. In **File Explorer**, right click the project and choose **TortoiseGit** ****Pull**.
2. Choose origin and branch and click **OK**.
3. Close the log.

##### External tool - Command line

Switch to the local repository and type `git pull`.

#### SVN

In SVN terminology, this process is known as *svn update*.

##### Eclipse plugin - Subclipse

Right click the project name in **Project Explorer**, and choose **Team** ****Update to HEAD** from the context menu.

##### External tool - TortoiseSVN

In **File Explorer**, right click the project directory and choose **SVN Update** from the context menu.

##### External tool - Command line

Move to the project directory and type `svn update`.

### Committing into repository

| [Git](server-projects-versioning.md#git) |
| --- |
| [SVN](server-projects-versioning.md#svn) |

To commit changes into repository, you should have a versioned server project. You can either create a new one (see [Adding server project to version control](server-projects-versioning.md#adding-server-project-to-version-control)) or check out an existing one (see [Initial check-out of project from repository](server-projects-versioning.md#initial-check-out-of-project-from-repository)).

#### Git

##### Eclipse plugin - EGit

1. Right click the project in **Project Explorer**, and choose **Team** ****Commit**.
2. Choose files, enter a commit message, and click **Commit and Push**.
3. Enter credentials.
4. View the changes and click **OK**.

##### External tool - TortoiseGit

1. In **File Explorer**, right click the project and choose **Git commit → "master"**.
2. Type the commit message, choose files to be committed and click **Commit**.
   You can change **Commit** to **Commit & Push**.

##### External tool - Command line

1. Add changes to *staging area*.
   Within the repository, type `git add path/to/file(s)`.
2. Type `git commit -m "The commit message"` to commit the changes.
3. Type `git push` to push the changes to the remote repository.

#### SVN

##### Eclipse plugin - Subclipse

1. In the **Project Explorer** view, right click the project name and choose **Team** ****Commit…​**
2. Type the *commit message*, choose files to be committed, and click **OK**.

##### External tool - TortoiseSVN

1. In **File Explorer**, right click the project directory and choose **SVN Commit…​**
2. Choose the files to be committed, type a commit message and click **OK**.

##### External tool - Command line

1. Add files that you added with `svn add path/to/file`.
2. Type `svn commit -m "The commit message"` to commit the changes.
