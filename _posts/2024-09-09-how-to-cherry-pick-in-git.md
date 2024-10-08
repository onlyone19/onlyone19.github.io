---
title: How to Cherry-Pick in GIT
category: Blog
tags:
  - tools
  - git
---

## What is Cherry-Pick
Simply put, cherry-pick is picking a single commit from one branch and put that commit to a different branch.

1. Checkout the branch you want to put the commit to. In our case, we want the commit to go to master.
    ```bash
    git checkout master
    ```

2. Now we need to create a branch off of master to put our cherry-picked commit to. So, the next step is to create a new branch from master.
    ```
    git checkout -b cherry-pick-commit
    ----or----git branch cherry-pick-commit
    git checkout cherry-pick-commit
    ```
  
3. Now it’s time to cherry-pick our commit. For that, you only need the SHA of the commit which you can get from the git GUI or by command line through git log command. The commit SHA is generally veryyyyyy long but for simplicity, I have denoted the commits with just single alphabets.
    ```
    git cherry-pick hsaofacommit
    ```

4. Now you have the cherry-picked commit in your cherry-pick-commit branch. Now push the changes to your repo.
    ```
    git push origin cherry-pick-commit
    ```

5. Create a PR with the base branch as master, merge it and you’re done.
