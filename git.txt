Git 


Add local repository to github:
create empty repository on GitHub. 

then on your local machine:
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/rutgerhofste/cheatsheets.git
git push -u origin master


Create and switch to new branch
git branch branchname
git checkout branchname

Check HEAD
git log --oneline --decorate

Merge branch:
git checkout master
$ git merge branchname


Delete branch:
git branch -d hotfix

Sync from remote branch 
git fetch 
git merge 

git pull = git fetch + git merge


