# Introduction

# 1. Basics
## 1.1 Git from an existing local directory
Go to a reportory :
```bash
cd my-repo-git
```

Init a git repositery :
```git
git init
```

Add a file in the repositery :
```git
git add Makefile
```

If we check the status you will see that Makefile is added but not the other
files :
```git
git status
```


Add multiple files :
```git
git add license.txt LICENSE
git add *
```

By checking again the status we will see that all the files are added but not
commited :
files :
```git
git status
```

Valide the modification :
```git
git commit
```

Now all files are commited :
```git
git status
```

The files are only locally on master we need to push the changes on the
distant repositery. If we push directly the master it will tell you that
it doesn't know the distant repositery :
```git
git push
```

If the repositery is on Github, we can add it by:
```git
git remote add origin git@github.com:username/repository.git
```

Now if we push, we will a message saying that the distant branch doesn't
exist :
```git
git push
```

We can create it by doing only once :
```git
git push --set-upstream origin master
```

## 1.2 Git from a distant repositery
If the repositery already exists you can clone it:
```git
git clone git@github.com:/repository.git
```
If you don't have the push rights, you will have to push on your own private
repositery. On Github you can fork a repositery easily by clicking on the
fork button.

## 1.3 Git branches
On the master branch, we push only workings version of the repositery. Thus,
if we want to modify something or add a new feature, we must create and work on
a new branch.

Create a branch :
```git
git branch branch_name
```

Show all the branches on a repositery :
```git
git branch
```

Change the branch :
```git
git checkout branch_name
```

After we have done all the modification we need, we must push the
modification on the branch. For that we add the files and then commit them :
```git
git add README.md
git commit
```

As it's boring to add each file seperatly and then commit them, it's possible
to commit all the changed files :
```git
git commit -a
```

If the only change I have done is a small fix and I don't want to add a
specific commit for that, I can add it to the previous commit :
```git
git commit -a --amend
```

As before the branch is only local, if I want to share it with someone else :
```git
git push --set-upstream origin test
```

## 1.4 Fetch the data from a distant branch
If I want to copy the data from a distant branch :
```git
git fetch origin branch-name
```

This command will put branch-name in memory on a virtual branch FETCH_HEAD.
If I want to create a copy of FETCH_HEAD
```git
git commit -b copy_name FETCH_HEAD
```

If someone else has pushed some modification on the distant branch I can
recover them :
```git
git fetch origin branch-name
git rebase origin/branch-name
```
**Always use a rebase on that case.**

### What is the difference between rebase and merge ?
Let's consider the following case :

If we do a merge, we merge the commit of the origin/branch_name with the last
commit of our branch_name branch.
Thus, if we want to change one of our previous commit it could be a problem.
We will use this option mainly to merge a branch to another.

If we do a rebase, we change the origin of our branch_name to be the end of
origin/branch_name. With that we can conserve all the previous commit.

**If we want to merge the evolution of a branch to another we must be sure
the end of branch_destination is the begining of the branch_origin. If it's not
the case, we must use a rebase**:
```git
git merge branch_origin branch_destination
```

It possible to remove, squash any of the commit by :
```git
git rebase -i branch_name
```

If I want to do it for the previous commit on my branch :
```git
git rebase -i HEAD~8
```

### Solve conflicts
When you try a rebase, some conflicts can be launched. You must solve the
problem and then says to git they are solved:
```git
git add conflict_file
git rebase --continue
```

As we said before, it's better to merge a branch only they are rebased.
In that way, it's easier to solve the conflicts and on that way we can conserve
all the successive modification.

### Issues and Pull Request on Linux

### Git configuration
You can define some personal git properties as alias for exemple. To do it,
you have to create a file called ``~/.gitconfig``. We provide an example of
that file :
```
[color]
  branch = true
  diff = true
  interactive = true
  ui = true
  status = true

[core]
  editor = vim
  preloadindex = true
  autocrlf = false
  whitespace = trailing-space,space-before-tab,indent-with-non-space

[alias]
  ci = commit
  co = checkout
  st = status
  br = branch

[user]
  name = Thierry Guillemot
  email = thierry.guillemot.work@gmail.com

[push]
  default = simple
```
