## 远程repository改名

改了github repository名称以后，需要进本地repository的git config执行

git remote set-url origin 新的git url

## Undo Git Init

The Git command line does not give us a “git init undo” command. This is because undoing a git init operation is as simple as removing the .git/ folder.
We can remove this folder using the rm -rf command :
rm -rf .git/