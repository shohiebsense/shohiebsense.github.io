#### 1\. Make a pre-commit git hook

[Prevent Accidental Commit to Master and Dev Branch in GIT](https://www.cyberithub.com/how-to-prevent-accidental-commit-to-master-and-dev-branch-in-git/)

Make a file named pre-commit

```.sh
#!/bin/sh

branch="$(git rev-parse --abbrev-ref HEAD)"

if [ "$branch" = "development" ]; then
  echo "Dev Branch commit is blocked"
  exit 1
fi

if [ "$branch" = "master" ]; then
  echo "Master Branch commit is blocked"
  exit 1
fi

if [ "$branch" = "deployment-test" ]; then
  echo "Deployment Test commit is blocked"
  exit 1
fi
```
adjust the branches' names to protect so that they suit your development.

`git rev-parse --abbrev-ref HEAD` is to know the current branch.


#### 2\. Since Git Hook runs locally, share to your team.

[Here's how](https://www.viget.com/articles/two-ways-to-share-git-hooks-with-your-team/)

Check your git versions first, If it is 2.9 or greater, it will be more convenient.

I do the same as the article above, put the hook files inside `$project_root/.githooks/`

```git
$ git config core.hooksPath .githooks
```

then create `Makefile`, add this script 

```Makefile
init:
  git config core.hooksPath .githooks
```


#### 3\. Apply Branch protection rule

like, only accepts pull request, and must up to date branch with the target (master/main/development) first.

![BranchProtectionRule](https://i.postimg.cc/sXKFGBsX/2022-03-23-11-15-32-New-branch-protection-rule-Mozilla-Firefox.png)

If it clashes with the product team rule (e.g "hold this module first before that", then the task is to regulate the branch to be always up-to-date.  
Use tags for helpers. Say you name it "postponed".  
Every time the staging-production branch is updated, you have to pull to postponed.  
My takes there, will be a bit of hassle, but it will save your precious time when you really need it.  
If you had been there, you really know what I'm saying o_O
