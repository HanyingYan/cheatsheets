## 1. Background
Git is a ***distributed version control system*** that tracks changes in any set of computer files.
It is usually used for coordinating work among programmers collaboratively developing source code during software development. 

**Origin**: a shorthand name for the remote repository that a project was originally cloned from. It is used instead of the ***original repository's URL*** to make referencing much easier.

**Remote Branch**: a reference to the state of the branches in a remote repository (a version of your project hosted on the internet or on a network like GitHub). When you clone a repository, you pull data from a repository on the internet or an internal server known as the remote (similar to ```(remote)/(branch)```)

**HEAD**: only one branch can be checked out at a time with git - and this is what's called the ***HEAD*** branch. It's also referred to as the ***active*** or ***current*** branch.


## 2. Commands
### A. Create Snapshots
1. Initialize a repository
```git init```
2. Stage files<br/>
  ```git add <file_name>                      # Stages a single file``` <br/>
  ```git add <file_name_1> <file_name_2>      # Stages multiple files``` <br/>
  ```git add <pattern>                        # Stages with a pattern```<br/>
  ```git add .                                # Stages the current directory and all its content```
3. View the status<br/>
  ```git status              # Full status```<br/>
  ```git status -s           # Short status```
4. Commit the staged files<br/>
  ```git commit -m “<msg>”   # Commit with a one-line message```<br/>
  ```git commit               #Opens the default editor to type a long message```
5. Skip the staging area<br/>
  ```git commit -am “<msg>”```
6. Remove files <br/> 
  ```git rm <file_name>              # Removes from working directory and staging area```<br/>
  ```git rm --cached <file_name>     # Removes from staging area only```
7. Rename or move files  
  ```git mv <file_name_1>  <file_name_2>```
8. View the staged/unstaged changes <br/> 
  ```git diff            # Shows unstaged changes```<br/>
  ```git diff --staged   # Shows staged changes```<br/>
  ```git diff --cached   # Same as the above```
9. View the history <br/> 
  ```git log                  # Full history```<br/>
  ```git log --oneline        # Summary```<br/>
  ```git log --reverse        # Lists the commits from the oldest to the newest```
10. View a commit<br/>
  ```git show <commit_id>          # Shows the given commit```  
  ```git show HEAD                 # Shows the last commit```<br/> 
  ```git show HEAD~2               # Two steps before the last commit```<br/> 
  ```git show HEAD:<file_name>     # Shows the version of <file_name> stored in the last commit```
11. Unstage files (undoing git add)<br/>
  ```git restore --staged <file_name>   # Copies the last version of <file_name> from repo to index```
12. Discard local changes <br/>
  ```git restore <file_name>                  # Copies <file_name> from index to working directory```<br/>
  ```git restore <file_name_1> <file_name_2>  # Restores multiple files in working directory```<br/>
  ```git restore .                            # Discards all local changes (except untracked files)```<br/>
  ```git clean -fd                            # Removes all untracked files```
13. Restore an earlier version of a file  
```git restore --source=HEAD~2 <file_name> ```

### B. Branch and Merge
1. Manage branches<br/>
```git branch dev           # Creates a new branch called dev```<br/>
```git checkout dev         # Switches to the branch```<br/>
```git switch dev           # Same as the above```<br/>
```git switch -C dev        # Creates and switches```<br/>
```git branch -d dev        # Deletes the branch```
2. Compare branches<br/>
```git log master..dev      # Lists the commits in the dev branch not in master``` <br/>
```git diff master..dev     # Shows the summary of changes```
3. Merge<br/>
```git merge dev            # Merges the dev branch into the current branch```<br/>
```git merge --no-ff dev    # Creates a merge commit even if FF is possible```<br/>
```git merge --squash dev   # Performs a squash merge```<br/>
```git merge --abort        # Aborts the merge```
4. View the merged branches<br/>
```git branch --merged      # Shows the merged branches```<br/>
```git branch --no-merged   # Shows the unmerged branches```

### C. Collaboration
1. Clone a repository
```git clone url```
2. Sync with remotes<br/>
```git fetch origin master  # Fetches master from origin```<br/>
```git fetch origin         # Fetches all objects from origin``` <br/>
```git fetch                # Shortcut for “git fetch origin”```<br/>
```git pull                 # Fetch + merge```<br/>
```git push origin master   # Pushes master to origin```<br/>
```git push                 # Shortcut for “git push origin master”```
3. Share tags<br/>
```git push origin v1.0```<br/>
```git push origin -delete v1.0```
4. Share branches<br/>
```git branch -r            # Shows remote tracking branches```<br/>
```git branch -vv           # Shows local & remote tracking branches```<br/>
```git push -u origin dev   # Pushes dev to origin```<br/>
```git push -d origin dev   # Removes dev from origin```
5. Manage remotes<br/>
```git remote                    # Shows remote repos```<br/>
```git remote show origin        # Shows remote origin repo```<br/>
```git remote add upstream url   # Adds a new remote called upstream```<br/>
```git remote rm upstream        # Remotes upstream```
