# Advanced Software Engineering

## Katalon Studio - Git Integration

### Create a Remote Repository from an Existing Project

1. **Enable Git Integration**
   - Ensure that Git integration is enabled in Katalon Studio. This is typically indicated by a Git icon or toolbar button.

2. **Check for Advanced Configurations**
   - Verify that all necessary advanced Git configurations are set up according to your project's needs.

3. **Share Project (git init)**
   - Initialize Git in your existing Katalon project. This can usually be done via the Katalon Studio interface by selecting `Git > Share Project` or similar options, which runs `git init` in the background.

4. **Create Bitbucket Repo (empty & copy URL)**
   - Go to Bitbucket and create a new repository. Ensure it's an empty repository, then copy the repository URL provided.

5. **“Initial commit” (commit & push to the URL)**
   - Make the initial commit of your project to the Bitbucket repository:
     - Add all files: `git add .`
     - Commit changes: `git commit -m "Initial commit"`
     - Add the remote repository URL: `git remote add origin <your-repo-url>`
     - Push to the remote repository: `git push -u origin master`

   At this point, your local repository should be connected to the remote repository with an initial commit.

### Manage Branches

1. **Create a New Branch & Checkout**
   - Create and switch to a new branch: `git checkout -b <branch-name>`

2. **Add a New Test Case (commit & push)**
   - Add your test case changes.
   - Stage the changes: `git add <changed-files>`
   - Commit the changes: `git commit -m "Add new test case"`
   - Push the branch to the remote repository: `git push origin <branch-name>`

3. **Create Pull Request & Merge/Close (server side)**
   - Go to your Bitbucket repository and create a pull request from your branch to the `master` branch.
   - Review and merge the pull request on the server-side as required. Optionally, close the pull request if it's not needed.

4. **Pull Changes from Server - Branch Master**
   - Switch to the master branch: `git checkout master`
   - Pull the latest changes: `git pull origin master`

5. **Delete the Local Branch**
   - Delete the local branch: `git branch -d <branch-name>`

   Optionally, delete the remote branch if no longer needed: `git push origin --delete <branch-name>`

   Fetching checks for existing changes and returns information about them. Use `git fetch` to retrieve updates without merging them automatically.

### Handle Conflicts

1. **Create a New Branch & Checkout**
   - Create and switch to a new branch: `git checkout -b <branch-name>`

2. **Edit the Same Test Case in Parallel**
   - Both you and your teammate edit the same test case in the same line but add different comments.

3. **Commit & Push Your Update**
   - Commit your changes: `git add <changed-files>` followed by `git commit -m "Your comment"`
   - Push to the remote repository: `git push origin <branch-name>`
   - If there’s a conflict with the push, Git will reject it.

4. **Create a New Branch & Checkout**
   - Again, create and switch to another new branch: `git checkout -b <branch-name>`

5. **Edit the Same Test Case**
   - Both you and your teammate repeat the changes as in step 2.

6. **Commit & Push Your Update**
   - Commit and push as done earlier. You might encounter conflicts if the changes from the other branch are also pushed or merged.

   **Resolve Conflicts:**
   - Pull the latest changes from the remote branch: `git pull origin <branch-name>`
   - Resolve conflicts manually in the files.
   - Add resolved files: `git add <resolved-files>`
   - Commit the resolution: `git commit -m "Resolve merge conflicts"`
   - Push the resolved branch: `git push origin <branch-name>`

Handling conflicts might require communication with your team to coordinate changes effectively.
