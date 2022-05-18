## github 连不上问题

unset remote origin proxy
unset httpserver
unset httpsserver
## 远程repository改名

改了github repository名称以后，需要进本地repository的git config执行

git remote set-url origin 新的git url

## Undo Git Init

The Git command line does not give us a “git init undo” command. This is because undoing a git init operation is as simple as removing the .git/ folder.
We can remove this folder using the rm -rf command :
rm -rf .git/

https://careerkarma.com/blog/git-undo-git-init/

## adding a local repository to github repository

https://docs.github.com/en/get-started/importing-your-projects-to-github/importing-source-code-to-github/adding-locally-hosted-code-to-github

git init -b main

git add . && git commit -m "initial commit"

git remote add origin  <REMOTE_URL> 

git remote -v

git push -u origin main

## if unsure whether main branch is called master or main

git show-ref 

can show whether heads is master or main

if master, use git push -u origin master

if main, use git push -u origin main

## forgotten remote origin and want to view

git remote -v