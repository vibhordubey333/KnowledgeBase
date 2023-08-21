# Git Commands.
* git branch -v
* git checkout -b new_branch_name  
* git checkout branch_to_switch
* git status
* git log
* git add .
* git commit -m "your_message"
* git push origin branch_name
* git diff
* git remote add origin https://github.com/vibhordubey333/GITCheatSheet.git
* git remote set-url origin https://github.com/vibhordubey333/GITCheatSheet.git
* git branch -d localBranchName  // delete branch locally 
* git push origin --delete remoteBranchName // delete branch remotely
* To sync changes with master branch or other branch -> git pull origin branch_name
* git pull origin branch_name
* Delete local branch [Forcefully] : git branch -D branch_name
* git commit --amend -m "New commit message."
* Removing Merge conflicts:
  - Configure "git mergetool"
  - Fire "git mergetool"
  - After conflicts are resolved do below.
    - git add .
    - git commit 
    - git push origin branch_name
 * To fetch remote refs,commits from remote
    - git fetch -a
 * Git Stash : https://www.linuxfordevices.com/tutorials/linux/git-stash
 * Merge Conflits Remocing Manually
   - Everything between <<<<<<< and ======= is what was in one file, and
   - Everything between ======= and >>>>>>> is what was in the other file
 * To resolve Carrige Return Line Feed [CRLF ] windows
   - git config --list
   - git config --global core.autocrlf false
 * To refer to private hosted library
   - git config --global url."git@github.org_name.com:".insteadof "https://github.org_name.com"
 * Configuring name and email in git.
    - Change Git user name by running: git config user.name “Your Name”
    - Change Git user email by running: git config user.email “name@email.com”
 * Checking code which went with the commit
    - git show HEAD
    - git show commit_id
 * Deleting branch
    - Remote: `git push origin -d Feature/SPR-1232`
    - Local:  `git branch -D Feature/SPR-12140`	
* Rebase [To sync the changes with other branch.]
    - git checkout feature/movies_comment
    - git rebase master
* Mistake in commit, not pushed 
    -Undo a commit & redo
     ` $ git commit -m "Something terribly misguided" # (0: Your Accident)
      $ git reset HEAD~                              # (1)
      [ edit files as necessary ]                    # (2)
      $ git add .                                    # (3)
      $ git commit -c ORIG_HEAD                      # (4)`
* Reverting the changes
    - git log -5
    - git reset HEAD~3
    - To push after reverting `git push -f origin branch_name`
    * Rollback the reverted changes
      - Exactly the same no. of times which you mentioned in reverting `git reset HEAD@3`
    * Delete the local branch then fetch the changes again for proper sync.
* Remove un-commited changes
    - git clean -fdx
* Remove file from commit [Not sure though, need to test]
    - git rm -r --cached file_name
    - https://stackoverflow.com/questions/37422221/git-remove-a-file-from-a-branch-keep-it-in-the-master
* Amend last commit or add new change into last commit, instead of creating one.
    -  [Original Post Link](https://medium.com/@igor_marques/git-basics-adding-more-changes-to-your-last-commit-1629344cb9a8)
    - `$ (some_branch) git add changelog.md`
    - If you will use this you can re-write new commit message, `(some_branch) git commit --amend`
    - Opt for this one if you don't intend to edit the last commit message `(some_branch) git commit --amend --no-edit`
    - Be careful ! mention the correct branch `$ (some_branch) git push -f origin some_branch`
* Remove file after performing `git add file_name`
    - `git reset file_name`
* Create a new branch and push it to remote repository
    - `git checkout -b Feature/Bug_ID`
    - `git push origin Above_created_Branch_Name`
* Error code's defined in GIT.
  ```#define Z_OK            0
   #define Z_STREAM_END    1
   #define Z_NEED_DICT     2
   #define Z_ERRNO        (-1)
   #define Z_STREAM_ERROR (-2)
   #define Z_DATA_ERROR   (-3)
   #define Z_MEM_ERROR    (-4)
   #define Z_BUF_ERROR    (-5)
   #define Z_VERSION_ERROR (-6)```
 * For Git error `fatal: pack has bad object at offset 196326059: inflate returned 1 fatal: fetch-pack: invalid index-pack output`
   ```
   git config --global core.compression 0
   git clone --depth 1 ssh://username@domain.com/path/to/git_repo/
   git fetch --unshallow //For retrieving rest of the repo
   git pull --all
   ```
   - May be you'll not be able to fetch all the branches inspite of doing `git pull --all` and `git fetch --all`.
   - Find the remote origin `git config --list` -> `remote.origin.url=git@github.org_name.com:org_name/repo_name.git`
   - `git remote set-url origin git@github.org_name.com:org_name/repo_name.git`
 * Set local repo configuration:<br/>
   -   `git config user.email="vibhordubey333@gmail.com" --local`<br/>
 
 * Handling multiple configurations in one machine<br/>
   - https://www.freecodecamp.org/news/how-to-handle-multiple-git-configurations-in-one-machine/<br/>
   - Note: When creating .gitconfig-perfonal/work enter 1 extra space <br/>

#### Issues:
  1. **unable to access Could not resolve proxy:**
     ```
     export http_proxy=""
     export https_proxy=""
     ```
