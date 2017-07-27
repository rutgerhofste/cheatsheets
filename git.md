Git 


Add local repository to github:
create empty repository. 

then on your local machine  
`git init`  
`git add README.md`  
`git commit -m "first commit"`  
`git remote add origin https://github.com/rutgerhofste/cheatsheets.git`  
`git push -u origin master`  

clone a remote repository:
'git clone <HTTPS or SSH from Github>'  

Work on repo  
`git status`
`git add .`  
`git commit -m "message"`  
`git push origin master`

Pull from origin  
`git pull origin`

Create and switch to new branch  
`git branch branchname`  
`git checkout branchname`  

Check HEAD  
`git log --oneline --decorate`

Merge branch  
`git checkout master`
`git merge branchname`  

Delete branch  
`git branch -d <branchname>`

Sync from remote branch 
`git fetch`   
`git merge`  

git pull = git fetch + git merge


