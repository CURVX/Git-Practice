## Useful commands
- `rmdir <directory>` : needs to be an empty directory
- `rm -rf <nonEmpty_directory>` : deletes the non-empty directory recursively without prompting anything.



## Git useful commands:
- `git init` : creates a hidden folder, .git, needed for Git to work.
- `git status` : review the list of files
- `git add <fileName1> <fileName2> <...>` : stage individual files 
- `git add .` : Adds all files
- `git commit -m '<message>'` : commit files staged with a message
- `git remote add origin https://<userName/repository>.git`: You will first need to create an repository in your git service
- `git log @{upstream/u}` : what was done locally and not yet published, current branch
- `git show` : shows the commit message and a diff of the changes introduced
- `git show @~3` : shows the 3rd-from-last commit

## Quick Lins
- [Pushing](https://github.com/CURVX/Git-Practice#pushing)

### Setting username and email
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

### Log, shortlog and show

- `git log` : will display all your commits with the author and hash
- `git log -2` : list last 2 commit logs
- `git log --oneline` : will show all of your commits with only the first part of the hash and the commit message
- `git log -2 --oneline` : last 2 commit logs oneline
- `git shortlog` :  list of all commits made per committe
- `git show <hash>` : view contents of a single commit

#### Show the total number of commits per author
- `git shortlog -s` : provides the author names and number of commits by each one
- `git shortlog -s--all` : provides the author names and number of commits by each one on all branches
- `git shortlog-sn` : Names and Number of commits
- `git shortlog-sne` : Names along with their email ids and the Number of commits

### Remote
- `git remote` : shows the short name of each remote handle
- `git remote -v` : detailed information includes the URL and type of remote(push or pull)
- `git remote set-url`: 
#### Change git repository name
##### Change local setting
- `git remote set-url origin https://username@bitbucket.org/username/newName.git`
- `git remote -v` : to check again
- `git push`
#### Remove a Remote Repository
- `git remote rm <name>` : remove a remote repository
#### Rename a Remote Repository
- `git remote rename <old> <new>`
#### Show more information about remoterepository
- `git remote show origin`
#### Add a Remote Repository
- `git remote add <name> <url>`
The command git fetch<name> can then be used to create and update remote-tracking branches<name>/<branch>

### Cloning Repositories

The git clone command is used to copy an existing Git repository from a server to the local machine

- `git clone https://github.com/username/projectname.git`: clones the repo in your current directory.
- `git clone https://github.com/username/projectname.git MyFolder` : clones the repo into MyFolder in your current directory.

### Stashing TO_DO

### Renaming
- `git branch-m old_name new_name`: renaming a local branch
#### Renaming a local and the remote branch:
- Checkout from the branch
then rename the local branch, delete the old remote and set the new renamed branch as upstream:
```
git checkout old_branch
git branch-m new_branch
git push origin :old_branch
git push--set-upstream origin new_branch
```

### Pushing
- `git push<remotename> <object>:<remotebranchname>` : general syntax
#### Delete remote branch
- `git push <remotename> :<remotebranchname>` : Deleting the remote branch is the equivalent of pushing an empty object to it.
Example: `git push origin :wip-yourname`: will delete the remote branch wip-yourname
Instead of using the colon, you can also use the `--delete` flag, which is better readable in some cases.
Example: `git push origin --delete wip-yourname`

- `git push origin feature_x` : to push to a specific branch, for example: feature_x
#### Set the remote tracking branch
- `git push --set-upstream origin master` OR
- `git push -u origin master` ( -u as a shorthand for --set-upstream)
#### Pushing to a new repository
To push to a repository that you haven't made yet, or is empty:
- Create the repository on GitHub (if applicable).
- Copy the url given to you, in the form `https://github.com/USERNAME/REPO_NAME.git`.
- Go to your local repository, and execute `git remote add origin URL`.
- To verify it was added, run `git remote-v` Run git push origin master.
Your code should now be on GitHub

#### Force pushing
- `git push-f`: will overwrite any remote changes and your remote will match your local
Using this command may cause the remote repository to lose commits. Moreover, it is strongly advised
against doing a force push if you are sharing this remote repository with others, since their history will retain every
overwritten commit, thus rending their work out of sync with the remote repository.





### Blaming
#### Only show certain lines
- `git blame -L<start>,<end>` : Example `git blame -L 10,30`
- `git blame -L /regex/` : Example `git blame -L /void main/` and `git blame -L 46, /void foo/`

#### To find out who changed a file
- `git blame <filename>` : shows the author and commit per line of specified file
- `git blame -L 1,10 test.c` : limits the selection of lines by specified range

#### Archive
- `git archive --format zip HEAD > archive-HEAD.zip` : creates a zip archive of current HEAD revision
Alternatively it is possible to just specify an output file with valid extension and the format and compression typewill be inferred from it
- `git archive --output=archive-HEAD.tar.gz HEAD`
- `git archive --output=archive-HEAD.zip --prefix=src-directory-name HEAD` : When extracted all the files will be extracted inside a directory named src-directory-name in the current directory.


### Git useful notes:
git does not recognice the concept of folders, it just works with files and their filepaths. This means git does not track empty folders.
If you want to keep an directory that your application rely on for example 'build', a convention is to include a '.gitkeep' file inside the directory and let Git track that file.
```
git add build/.gitkeep
git commit-m 'Keep the build directory around'
````



