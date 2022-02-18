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
* Reverting the changes
    - git log -5
    - git reset HEAD~3
    - To push after reverting `git push -f origin branch_name`
    * Rollback the reverted changes
      - Exactly the same no. of times which you mentioned in reverting `git reset HEAD@3`
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
