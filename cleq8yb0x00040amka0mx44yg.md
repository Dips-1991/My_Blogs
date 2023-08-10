---
title: "Day 11 Task: Advance Git & GitHub for DevOps Engineers: Part-4"
datePublished: Wed Mar 01 2023 22:25:56 GMT+0000 (Coordinated Universal Time)
cuid: cleq8yb0x00040amka0mx44yg
slug: day-11-task-advance-git-github-for-devops-engineers-part-4
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1677709279202/73ff6cfb-29d7-4273-ad0f-7a65a2938cf4.jpeg
tags: devops-github-git-90daysofdevops-devops-articles

---

### **What is Git Stash:**

* Let's first discuss what we mean by *'****stash****'*, i.e. store something safely in a hidden place. Hence [`git stash`](https://www.golinuxcloud.com/git-stash-explained-in-detail-with-examples/) is a command temporarily saves your data without committing them. This is useful when you need to switch to a different branch to work on something else, but you don't want to commit the changes you've made in your current branch yet.
    
* To use *Git stash*, you first create a new branch and make some changes to it. Then you can use the command `git stash` to save those changes. This will remove the changes from your working directory and record them in a new stash.
    
* ***Git stash*** has the following options available
    
    * **git stash list:** This returns a list of your saved snapshots in the format `stash@{0}:`
        
        Syntax: **git stash list**
        
    * **stash pop:** To bring the changes back and apply them on top of the new commits.
        
        Syntax: **git pop**
        
    * **git stash apply:** Applies the changes and leaves a copy in the stash
        
        Syntax: **git stash apply &lt;stash-name&gt;**
        
    * **git stash or git stash save &lt;message&gt;:** Store the changes to (stash)
        
        Syntax: **git stash save &lt;message&gt;**
        
    * **git stash clear:** The git stash clear command allows deleting all the available stashes at once.
        
        Syntax: **git stash clear**
        
    * **git stash drop &lt;name of the stash&gt;:** To delete specific stash from the stash list
        
        Syntax: **git stash clear &lt;name of the stash&gt;**
        
    * **git stash branch &lt;branch-name&gt;:** which creates a new branch for you with your selected branch name
        
        Syntax: **git stash branch &lt;branch-name**
        

### ***What is Cherry-pick?***

* `git cherry-pick` is a command that allows you to pick specific commit from one branch and apply it to another. This can be useful when you want to selectively apply changes that were made in one branch to another.
    
* To use `git cherry-pick`, you first create two new branches and make some commits to them. Then you use the `git cherry-pick <commit_hash>` command to select the specific commits from one branch and apply them to the other.
    

### ***What is Resolving Conflicts?***

* Conflicts can occur when you merge or rebase branches that have diverged, and you need to manually resolve the conflicts before git can proceed with the merge/rebase.
    
* `git status` command shows the files that have conflicts, `git diff` the command shows the difference between the conflicting versions, and `git add` command is used to add the resolved files.
    

### ***Task-1***

1. **Create a new branch and make some changes to it**
    
2. **Use git stash to save the changes without committing them.**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677700249163/533ee66f-045c-47f2-bd90-316f4cae2bc5.png align="center")
    
3. **Switch to a different branch, make some changes, and commit them.**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677700599566/acf50181-afe4-437c-a228-f047db658cea.png align="center")
    
4. **Use git stash pop to bring the changes back and apply them on top of the new commits.**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677700986237/46d76f22-47df-4624-8044-635c003581a1.png align="center")
    

### ***Task-2***

**In version01.txt of development, branch add below lines after “This is the bug fix in development branch” that you added in Day10 and reverted to this commit.**

1. **Line2&gt;&gt; After bug fixing, this is the new feature with minor alteration”**
    
    **Commit this with message “ Added feature2.1 in development branch”**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677702241520/51c248e3-4494-4cdd-931f-016ba20ef3b1.png align="center")
    
2. **Line3&gt;&gt; This is the advancement of previous feature**
    
    **Commit this with message “ Added feature2.2 in development branch”**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677702485352/02f54e4c-11f9-47ed-a7fa-72689f5de4df.png align="center")
    
3. **Line4&gt;&gt; Feature 2 is completed and ready for release**
    
    **Commit this with message “ Feature2 completed”**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677702658018/b668d128-ac49-46c3-b8d1-279317bbb190.png align="center")
    
4. **All these commits messages should be reflected in Production branch too which will come out from dev branch (Hint: try rebase).**
    
    * Now here first we will check **all commits** in the dev branch
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677703079858/bf91fdb1-3d86-4f82-8786-ac8b6f24e7cc.png align="left")
        
    * Now here we will switch to the prod branch and will **use rebase command** to reflect all the dev branch commits in the prod branch
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677704674884/a1527a67-949b-4db6-b141-db04ea12b9d9.png align="center")
        
    
    ### ***Task-3***
    
    **In Production branch Cherry pick Commit “Added feature2.2 in development branch” and added the below lines in it:**
    
    * Here we will switch to the prod branch.
        
    * for cherry-pick we will use the command**: git cherry-pick &lt;commit ID of Added feature2.2 in development branch&gt;**
        
    * Here cherry-pick gives conflict error. so we need to solve conflict error.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677707770700/140bb43d-b70e-43e5-abcf-36cc65aa7629.png align="left")
        
    * After resolving the conflict error use the command **git cherry-pick &lt;commit ID&gt;** or **git cherry-pick --continue**
        
    * Now in git log you can see the commit is added at the top
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677708208786/4ccb13ac-90bf-4851-a773-432d2152e4d9.png align="left")
        
    
    **Line to be added after Line3&gt;&gt; This is the advancement of previous feature**
    
    **Line4&gt;&gt;Added few more changes to make it more optimized.**
    
    **Commit: Optimized the feature**
    
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677708844509/cca670b6-6104-4069-a10e-1f062db4688e.png align="center")
        
    
    **Thank you for reading the blog**
    
    **Happy Learning!**
    
    [**Devops**](https://akash-zade.hashnode.dev/tag/devops) [**GitHub**](https://akash-zade.hashnode.dev/tag/github) [**Git**](https://akash-zade.hashnode.dev/tag/git) [**#90daysofdevops**](https://akash-zade.hashnode.dev/tag/90daysofdevops) [**Devops articles**](https://akash-zade.hashnode.dev/tag/devops-articles)