This goes over the basics of using git, for a cheat sheet go [here](Git%20Cheatsheet.md)
# Git
Git is **version control** software. 
What that means is that you can make changes to files and directories, and save those changes.
After, you can revert changes if you don't like them.

There is a lot more that you can do with git, but those are the basics.

## Download Git
**`Winget`**
- `winget install --id Git.Git -e --source winget`

**`Windows Installer`**
- https://git-scm.com/downloads/win

**Restart your PowerShell to be able to use git CMD**

### Repositories
- This is the bread and butter of git.
- A repository is simply a directory (usually a project, but could be whatever you want) that is managed by git.
- Changes are **not saved automatically**.
- To save changes to any files, you have to *add the files to the staging area*, and then *commit* the changes.

### Areas in git
#### Working Directory
This is the directory on your local machine where you're actually making changes to your files.<br />
It's the **current state** of your project.

#### Staging (Index)
Intermediate area between the working directory and the git repository.<br />
When you use the command `git add`, any new, updated, or deleted files are moved to this area, preparing them to be committed
- *This does not remove them from your working directory or the repository, it simply shows you what files have changed.*

This allows you to selectively choose which changes you want to include in your next commit.

#### Local Repository
This is the `.git` directory on your local machine. When you do a `git commit`, changes from the staging area are permanently stored in your local repository's commit history.

#### Remote Repository
Version of the project hosted on a server (Ex. GitHub, GitLab, or Bitbucket)<br />
When you do `git push` you're sending commits from your local repository to the remote repository

### Branches
One of the key uses in git is branches. They allow you to manage versions of the project, and test out new features without changing the rest of the application (The **main** branch)<br />
You can **merge** these branches back into main if you want to update the main application

### General Workflow
1. Make changes to your files/project in the *Working Directory*
2. Use `git add` to add files to the *Staging* area.
3. Use `git commit` to save the changes to your *Local Repository*
4. Use `git push` to send the committed changes to your *Remote Repository*

### `.gitignore`
this is a file in your repository that specifies what files/directories/file types **git will not add** to the repository

- Typically, you will want to ignore **user preferences** such as the `.idea`, `.vs` and `.vscode` directories that different IDEs will create.
- If you are developing a **Web application**, make sure to add the `node_modules` directory
- If you are developing a **Java** application, add the compiled class files (`*.class`), log files (`*.log`) and package files (`*.jar`)
- If you are developing a **C#** application, add the `bin` and `obj` directories (`bin/` and `obj/`)
- If your project has a lot of image/video/document you don't want on the remote repository (they take up a lot of space), add them too

## GitHub
- GitHub allows you to use git to store, share and manage code over the web.
- To get started, make an account and visit your profile.

### Creating a GitHub Repository
1. Go to the **Repositories** tab
2. Click the green **New** button on the top right
3. Name it however you like
4. **Choose Private** unless you want anybody (even without a GitHub account) to be able to see what you put on it
	- If you are doing a public repository, **be very careful about committing sensitive information** as there are web scrapers that will steal that information, even if you have made commits after deleting the information. **Once it's out there, it's out there**.

5. (Optional) create a README file - this is just a `.md` file that contains basic info about your repository
6. (Optional) add a `.gitignore` - Pick from a selection of pre-made `.gitignore` templates. See [`.gitignore`](#`.gitignore`) for more details
7. (Optional) Choose a license - Tells others what you can and can't do with your code (usually not required unless you plan on making your code public)

### Cloning a repository on GitHub
**This is basically just downloading the code, but it also lets you make changes to the code on GitHub**

1. Navigate to the repository you want to clone
2. Click the green `<> Code` button in the top right
3. Copy the URL it gives you
4. Open PowerShell or Git Bash on your computer
5. Navigate to the directory you want to clone the repository to (Ex. `cd C:\sourcecode\`) - Use tab complete or copy the path from file explorer to speed this up
6. Navigate into the new directory that created (Ex. `cd \first-project\`)
7. You're all set up! Now you can do commands such as `add`, `commit` and `push` to make changes on your GitHub repository.
