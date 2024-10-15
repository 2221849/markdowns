# Advanced Software Engineering

## Git Concepts

### Creating a Git Repository

#### From Scratch (New and Empty)

1. **Creating a Directory and Initializing Git**

   To start a new Git repository from scratch, follow these steps:

   ```sh
   mkdir myfirstgitrepo
   cd myfirstgitrepo
   git init
   ```

   - `mkdir myfirstgitrepo` creates a new directory named `myfirstgitrepo`.
   - `cd myfirstgitrepo` navigates into this directory.
   - `git init` initializes a new Git repository within this directory, creating a `.git` subdirectory that contains Git metadata.

2. **Verifying Initialization**

   To confirm that Git has been initialized, you can list the contents of the `.git` directory:

   ```sh
   ls -al .git
   ```

   - This command shows hidden files and directories within `.git`, which include various Git configuration and tracking files.

#### Cloning an Existing Repository

1. **Cloning the Repository**

   To clone an existing repository, use:

   ```sh
   git clone https://github.com/udacity/course-git-blog-project
   cd course-git-blog-project
   ```

   - `git clone <URL>` creates a local copy of the repository at the specified URL, including all files, branches, and commit history.
   - `cd course-git-blog-project` changes into the directory of the cloned repository.

2. **Checking Contents**

   After cloning, you can list the files in the repository:

   ```sh
   ls -al
   ```

   - This command displays all files and directories in the cloned repository.

#### Checking Status

1. **Viewing Status**

   To see the status of your working directory and staging area:

   ```sh
   git status
   ```

   - This command shows which files are staged for the next commit, which files have changes not yet staged, and which files are untracked.

### Reviewing Git History

#### Showing Commit Logs

1. **Viewing Logs**

   To view the commit history:

   ```sh
   git log
   ```

   - This command displays a detailed list of commits in the current branch, showing commit IDs, authors, dates, and messages.

2. **Viewing Logs in Different Formats**

   - **One Line per Commit**

     ```sh
     git log --oneline
     ```

     - This option shows each commit as a single line with a shortened SHA hash and the commit message.

   - **Showing Modified Files**

     ```sh
     git log --stat
     ```

     - This format displays a summary of changes for each commit, including modified files and the number of lines added or deleted.

   - **Showing Detailed Changes**

     ```sh
     git log -p
     ```

     - This option shows the differences introduced by each commit, including detailed line-by-line changes.

#### Showing Details of a Specific Commit

1. **Viewing Commit Details**

   To see detailed information about a specific commit:

   ```sh
   git show <SHA>
   ```

   - Replace `<SHA>` with the commit hash to view detailed information, including the commit message and changes made.

### Commits

#### Staging Changes

1. **Adding Files to the Staging Area**

   To stage changes before committing:

   ```sh
   git add <file1> <file2> ... <fileN>
   ```

   - `git add` stages changes to be included in the next commit. You can specify individual files or use `.` to add all changes in the current directory.

#### Committing Changes

1. **Committing Staged Changes**

   To commit the staged changes:

   ```sh
   git commit -m "Initial commit"
   ```

   - `git commit -m "message"` records the changes with a descriptive commit message.

2. **Viewing Changes Before Committing**

   To review changes before committing:

   ```sh
   git diff
   ```

   - This command shows differences between the working directory and the index (staged changes).

#### Good Commit Messages

- **Do**: Keep commit messages short (under 60 characters), and describe what the commit does. For example, "Add new sidebar to the homepage."

- **Do Not**: Avoid explaining why or how changes were made, and avoid using "and" in commit messages. If "and" appears, consider breaking changes into separate commits.

### Ignoring Files

**.gitignore File**  

- **Purpose**: The `.gitignore` file specifies files or directories that Git should ignore. This is useful for excluding temporary or build files.

1. **Example .gitignore File**

   ```gitignore
   *.log
   node_modules/
   dist/
   ```

   - `*.log` ignores all `.log` files.
   - `node_modules/` ignores the `node_modules` directory, commonly used in JavaScript projects.
   - `dist/` ignores the `dist` directory, often used for build outputs.

### Tagging, Branching, and Merging

#### Tagging

1. **Adding a Tag**

   To create a tag for a specific commit:

   ```sh
   git tag -a v1.0 <SHA>
   ```

   - `git tag -a <tagname> <SHA>` creates an annotated tag pointing to a commit identified by `<SHA>`. Annotated tags include additional metadata.

2. **Listing Tags**

   To view all tags in the repository:

   ```sh
   git tag
   ```

   - This command lists all tags.

3. **Deleting a Tag**

   To remove a tag:

   ```sh
   git tag -d v1.0
   ```

   - `git tag -d <tagname>` deletes the specified tag locally.

#### Branching

1. **Listing Branches**

   To see all branches:

   ```sh
   git branch
   ```

   - This command lists branches, with the current branch indicated by an asterisk.

2. **Creating a Branch**

   To create a new branch:

   ```sh
   git branch sidebar
   ```

   - `git branch <branchname>` creates a new branch.

3. **Switching Branches**

   To switch to a different branch:

   ```sh
   git checkout sidebar
   ```

   - `git checkout <branchname>` switches to the specified branch.

4. **Deleting a Branch**

   To delete a branch:

   ```sh
   git branch -d sidebar
   ```

   - `git branch -d <branchname>` deletes the specified branch. Use `-D` to force deletion if the branch has unmerged changes.

#### Merging

1. **Regular Merge**

   To merge one branch into another:

   ```sh
   git merge <branchname>
   ```

   - `git merge <branchname>` combines changes from the specified branch into the current branch.

2. **Fast-Forward Merge**

   A fast-forward merge occurs when the branch being merged is directly ahead of the current branch:

   ```sh
   git merge <branchname>
   ```

   - Git simply moves the branch pointer forward.

#### Resolving Conflicts

1. **Identifying Conflicts**

   Conflicts occur when changes in different branches affect the same lines of code. Git marks these conflicts in the files with special markers (`<<<<`, `====`, `>>>>`).

2. **Resolving Conflicts and Committing**

   - Edit conflicted files to remove conflict markers and decide which changes to keep.
   - Stage resolved files:

     ```sh
     git add <file>
     ```

   - Commit the resolution:

     ```sh
     git commit -m "Resolved merge conflict in <file>"
     ```

### Basic Git Workflow

1. **Cloning a Repository**

   To create a local copy of a remote repository:

   ```sh
   git clone <url>
   ```

2. **Adding Files Locally**

   Add or modify files as needed in your local repository.

3. **Pushing Changes**

   To push changes to the remote repository:

   ```sh
   git push origin master
   ```

   - `git push` uploads your local commits to the specified remote branch.

4. **Pulling Changes**

   To update your local branch with changes from the remote repository:

   ```sh
   git pull --all
   ```

   - `git pull` fetches and merges changes from the remote repository.

5. **Using Branches for Features**

   Create branches for new features or fixes to keep the main branch stable.

### Git Workflows

#### Centralized Workflow

- **Overview**: In this workflow, all changes are committed directly to the master branch. Suitable for small teams but can become a bottleneck as team size increases.

#### Feature Branching

- **Overview**: Develop features in separate branches to keep the master branch clean. Each feature or bugfix is isolated in its own branch, making integration smoother.

#### GitFlow

- **Overview**: A structured branching model that includes branches for features, releases, and hotfixes. It’s ideal for larger projects with planned release cycles.

#### Forking Workflow

- **Overview**: Each developer works in their own fork of the repository. Common in open-source projects where contributors do not have direct push access to the main repository.

### Feature Branches and Pull Requests

#### Creating a Feature Branch

1. **Branch Creation**

   To create and switch to a new branch for a feature:

   ```sh
   git checkout -b feature-branch
   ```

2. **Development and Commits**

   Develop your feature, then stage and commit changes:

   ```sh
   git add .
   git commit -m "Add feature"
   ```

3. **Push and Create Pull Request**

   - **Push Branch**:

   ```sh
   git push origin feature-branch
   ```

   - **Create Pull Request**: Use the remote repository interface to open a pull request, requesting code review and merging into the main branch.

#### Review and Merge

1. **Review Process**

   - Team members review the pull request, discuss changes, and suggest improvements.

2. **Merging**

   - Once approved, the pull request is merged into the main branch, completing the feature integration.
