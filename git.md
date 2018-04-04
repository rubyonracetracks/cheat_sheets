# Git/GitHub Cheat Sheet

## Syncing a Fork
* https://help.github.com/articles/configuring-a-remote-for-a-fork/
* https://help.github.com/articles/syncing-a-fork/#platform-linux

## Cloning the Remote Branch (alt_branch)

    git checkout alt_branch
	
## Updating the Remote Branch to Include Master Branch Changes

    git checkout alt_branch
    git merge master
    git push origin alt_branch
    
## Deleting Remote Branch

    git push origin --delete alt_branch

## Pushing Project to Non-Empty Repository
```
# cd into the project directory
git init
git remote add origin <GitHub URL>
git fetch
git branch master origin/master
git checkout master
git add .
git commit -m 'Initial commit'
git push origin master
```
