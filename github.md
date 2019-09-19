# Github Cheat Sheet for stupid Xueyan

```Git
git add . 
git commit -m "message"
git push origin branch-name
```

```Git
# Duplicating a repository
git clone --bare https://github.com/exampleuser/old-repository.git
cd old-repository.git
git push --mirror https://github.com/exampleuser/new-repository.git
rm -rf old-repository.git
```
