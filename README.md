## Git useful commands:
- git init: creates a hidden folder, .git, needed for Git to work.
- git status: review the list of files
- git add <fileName1> <fileName2> .... : stage individual files 
- git add . : Adds all files
- git commit -m '<message>': commit files staged with a message
- git remote add origin https://link.git `You will need to create an repository`
- git log @{upstream/u}: what was done locally and not yet published, current branch
- git show: shows the commit message and a diff of the changes introduced
- git show @~3: shows the 3rd-from-last commit

### Pushing
- git push<remotename> <object>:<remotebranchname>: general syntax
#### Delete remote branch
- git push<remotename> :<remotebranchname>: Deleting the remote branch is the equivalent of pushing an empty object to it.
Example: `git push origin :wip-yourname`: will delete the remote branch wip-yourname
Instead of using the colon, you can also use the --delete flag, which is better readable in some cases.
Example: `git push origin --delete wip-yourname`

- git push origin feature_x: to push to a specific branch, for example: feature_x
#### Set the remote tracking branch
- git push --set-upstream origin master OR
- git push -u origin master ( -u as a shorthand for --set-upstream)




### Blaming
#### Only show certain lines
- git blame -L<start>,<end>: example `git blame -L 10,30`
- git blame -L /regex/: example `git blame -L /void main/` and `git blame -L 46, /void foo/`

#### To find out who changed a file
- git blame <filename>: shows the author and commit per line of specified file
- git blame -L 1,10 test.c: limits the selection of lines by specified range

#### Archive
- git archive --format zip HEAD > archive-HEAD.zip: creates a zip archive of current HEAD revision
Alternatively it is possible to just specify an output file with valid extension and the format and compression typewill be inferred from it
- git archive --output=archive-HEAD.tar.gz HEAD
- git archive --output=archive-HEAD.zip --prefix=src-directory-name HEAD: When extracted all the files will be extracted inside a directory named src-directory-name in the current directory.

### Remote
- git remote: shows the short name of each remote handle
- git remote -v: detailed information includes the URL and type of remote(push or pull)
#### Change git repository name
##### Change local setting
- git remote set-url origin https://username@bitbucket.org/username/newName.git
- git remote -v: to check again
- git push
#### Remove a Remote Repository
- git remote rm <name>: remove a remote repository
#### Rename a Remote Repository
- git remote rename <old> <new>
#### Show more information about remoterepository
- git remote show origin
#### Add a Remote Repository
- git remote add <name><url>
The command git fetch<name> can then be used to create and update remote-tracking branches<name>/<branch>


#### Show the total number of commits per author
- git shortlog-s: provides the author names and number of commits by each one
- git shortlog-s--all: provides the author names and number of commits by each one on all branches
- git shortlog-sn: Names and Number of commits
- git shortlog-sne: Names along with their email ids and the Number of commits

### Git useful notes:
git does not recognice the concept of folders, it just works with files and their filepaths. This means git does not track empty folders.
If you want to keep an directory that your application rely on for example 'build', a convention is to include a '.gitkeep' file inside the directory and let Git track that file.
`
git add build/.gitkeep
git commit-m 'Keep the build directory around'
`



