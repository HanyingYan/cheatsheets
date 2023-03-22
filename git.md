## 1. Background
Git is a ***distributed version control system*** that tracks changes in any set of computer files.
It is usually used for coordinating work among programmers collaboratively developing source code during software development. 


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


