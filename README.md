## Useful commands
- `rmdir <directory>` : needs to be an empty directory
- `rm -rf <nonEmpty_directory>` : deletes the non-empty directory recursively without prompting anything.



## > Git useful commands:
- `git init` : creates a hidden folder, .git, needed for Git to work.
- `git status` : review the list of files
- `git add <fileName1> <fileName2> <...>` : stage individual files 
- `git add .` : Adds all files
- `git commit -m '<message>'` : commit files staged with a message
- `git remote add origin https://<userName/repository>.git`: You will first need to create an repository in your git service
- `git log @{upstream/u}` : what was done locally and not yet published, current branch
- `git show` : shows the commit message and a diff of the changes introduced
- `git show @~3` : shows the 3rd-from-last commit

## > Quick Links
- [Pushing](https://github.com/CURVX/Git-Practice#pushing)

## > Setting username and email
That will allow commits to have the right author name and email associated to them and has nothing to do with authentication when pushing to a remote repository.

- To declare that identity for all repositories, use `git config--global`

```
git config--global user.name "Your Name"
git config--global user.email mail@example.com
```
- To declare an identity for a single repository, use `git config` inside a repo

```
cd/path/to/my/repo
git config user.name "Your Login At Work"
git config user.email mail_at_work@example.com
```

## > Log, shortlog and show

- `git log` : will display all your commits with the author and hash
- `git log -2` : list last 2 commit logs
- `git log --oneline` : will show all of your commits with only the first part of the hash and the commit message
- `git log -2 --oneline` : last 2 commit logs oneline
- `git shortlog` :  list of all commits made per committe
- `git show <hash>` : view contents of a single commit

### Show the total number of commits per author
- `git shortlog -s` : provides the author names and number of commits by each one
- `git shortlog -s--all` : provides the author names and number of commits by each one on all branches
- `git shortlog-sn` : Names and Number of commits
- `git shortlog-sne` : Names along with their email ids and the Number of commits

## > Remote
- `git remote` : shows the short name of each remote handle
- `git remote -v` : detailed information includes the URL and type of remote(push or pull)
- `git remote set-url <origin/alias> https://github.com/username/repo.git`: change 'origin' remote's URL/ set URL for a specific remote
- `git remote get-url <name>` : url for an existing remote
- `git remote show origin` : lists the URL for the remote repository as well as the tracking branch information
### Remove a Remote Repository
- `git remote rm <name>` : remove a remote repository
### Rename a Remote Repository
- `git remote rename <old> <new>` : change the alias/shortname, for example; origin to destination 
### Show more information about remoterepository
- `git remote show origin`
### Add a Remote Repository
- `git remote add <shortname> <url>`
The command git fetch<name> can then be used to create and update remote-tracking branches<name>/<branch>


## > Staging
- `git add .`: will stage all changes to files in the current directory
- `git reset <filePath>` : unstage a file that contains changes
- `git diff` : displays what will be committed
- `git rm --cached <filename>` : delete the file from git without removing it from disk

## > Undoing
To jump back to a previous commit, first find the commit's hash using `git log`.
- `git reset--soft <hash>` : To roll back to a previous commit <hash> while keeping the changes
- `git reset--soft HEAD~<n>` : roll back to last commit, here <n> is the value for unwinding the last n commits
- `git reset--hard <hash>` : to permanently discard any changes made after a specific commit
- `git reset--hard HEAD~<n>` : permanetly discard any changes made after the last commit, here <n> is the value for unwinding the last n commits

While you can recover the discarded commits using `reflog` and `reset`, uncommitted changes cannot be recovered. Use `git stash`; `git reset` instead of `git reset --hard` to be safe.

### Using reflog

- `git reflog`: if you screw up a rebase, one option to start again is to go back to the commit (pre rebase). You can do this usingreflog (which has the history of everything you've done for the last 90 days - this can be configured)

- `git checkout HEAD@{3}` : to create a new branch. Now you could delete the screwed up branch OR
- `git reset --hard HEAD@{3}` : reset directly back to a point in your `reflog`. There is no turning back so be 100% sure.

## > Merging

- `git merge <another_branch>` : make sure you are in the branch that is getting merged into.
- `git merge --abort` : after starting a merge, you might want to stop the merge and return everything to its pre-merge state
- `git merge<branch_name>--no-ff-m"<commit message>"` : merge with a commit as default behaviour in fast-forward only updates the branch pointer without creating a merge commit.

## > Committing

Commits with Git provide accountability by attributing authors with changes to code.

### Amending a commit

- `git commit --amend` : this will put the currently staged changes onto the previous commit

Note: This can also be used to edit an incorrect commit message. It will bring up the default editor and allow one to change the prior message.

- `git commit --amend -m "New message"` : specify the commit message

Note: Be aware that amending the most recent commit replaces it entirely and the previous commit is removedfrom the branch's history. This should be kept in mind when working with public repositories and on branches withother collaborators.

This means that if the earlier commit had already been pushed, after amending it you will have to `git push --force`.

### Commit message

- `git commit -m "Commit summary" -m "More detailed description follows here"` : can pass in multiple -m arguments



## > Cloning Repositories

The git clone command is used to copy an existing Git repository from a server to the local machine

- `git clone https://github.com/username/projectname.git`: clones the repo in your current directory.
- `git clone https://github.com/username/projectname.git MyFolder` : clones the repo into MyFolder in your current directory.

## > Stashing TO_DO

## > Renaming
- `git branch-m old_name new_name`: renaming a local branch
### Renaming a local and the remote branch:
- Checkout from the branch
then rename the local branch, delete the old remote and set the new renamed branch as upstream:
```
git checkout old_branch
git branch-m new_branch
git push origin :old_branch
git push--set-upstream origin new_branch
```

## > Pushing
- `git push<remotename> <object>:<remotebranchname>` : general syntax
### Delete remote branch
- `git push <remotename> :<remotebranchname>` : Deleting the remote branch is the equivalent of pushing an empty object to it.
Example: `git push origin :wip-yourname`: will delete the remote branch wip-yourname
Instead of using the colon, you can also use the `--delete` flag, which is better readable in some cases.
Example: `git push origin --delete wip-yourname`

- `git push origin feature_x` : to push to a specific branch, for example: feature_x
### Set the remote tracking branch
- `git push --set-upstream origin master` OR
- `git push -u origin master` ( -u as a shorthand for --set-upstream)
### Pushing to a new repository
To push to a repository that you haven't made yet, or is empty:
- Create the repository on GitHub (if applicable).
- Copy the url given to you, in the form `https://github.com/USERNAME/REPO_NAME.git`.
- Go to your local repository, and execute `git remote add origin URL`.
- To verify it was added, run `git remote-v` Run git push origin master.
Your code should now be on GitHub

### Force pushing
- `git push-f`: will overwrite any remote changes and your remote will match your local
Using this command may cause the remote repository to lose commits. Moreover, it is strongly advised
against doing a force push if you are sharing this remote repository with others, since their history will retain every
overwritten commit, thus rending their work out of sync with the remote repository.

## > Blaming


### Only show certain lines
- `git blame -L<start>,<end>` : Example `git blame -L 10,30`
- `git blame -L /regex/` : Example `git blame -L /void main/` and `git blame -L 46, /void foo/`

### To find out who changed a file
- `git blame <filename>` : shows the author and commit per line of specified file
- `git blame -L 1,10 test.c` : limits the selection of lines by specified range

### Archive
- `git archive --format zip HEAD > archive-HEAD.zip` : creates a zip archive of current HEAD revision
Alternatively it is possible to just specify an output file with valid extension and the format and compression typewill be inferred from it
- `git archive --output=archive-HEAD.tar.gz HEAD`
- `git archive --output=archive-HEAD.zip --prefix=src-directory-name HEAD` : When extracted all the files will be extracted inside a directory named src-directory-name in the current directory.


## > Git useful notes:
git does not recognice the concept of folders, it just works with files and their filepaths. This means git does not track empty folders.
If you want to keep an directory that your application rely on for example 'build', a convention is to include a '.gitkeep' file inside the directory and let Git track that file.

```
git add build/.gitkeep
git commit-m 'Keep the build directory around'
```

### Good commit messages

The seven rules of a great git commit message
1. Separate the subject line from body with a blank line.
2. Limit the subject line to 50 characters.
3. Capitalize the subject line.
4. Do not end the subject line with a period.
5. Use the imperative mood in the subject line.
6. Manually wrap each line of the body at 72 characters.
7. Use the body to explain what and why instead of how.

Examples:

```
TASK-123: Implement login through OAuth
TASK-124: Add auto minification of JS/CSS files
TASK-125: Fix minifier error when name > 200 chars
```
[Link 1](https://udacity.github.io/git-styleguide/)
[Link 2](https://chris.beams.io/posts/git-commit/)


