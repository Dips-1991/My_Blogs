---
title: "Day:12 Task:
Linux, Git, GitHub Command"
datePublished: Sun Mar 05 2023 17:50:25 GMT+0000 (Coordinated Universal Time)
cuid: clevove58000009mm9sap4wy9
slug: day12-task-linux-git-github-command
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678038261938/fd65ef5e-b057-4a5c-be41-902f204a09de.jpeg
tags: linux, github, git

---

Let's go through some Linux, Git, and Git-Hub useful Command

### **What is the command?**

A command is a specific instruction given to a computer application to perform some kind of task or function.

### **Linux Commands:**

1. **ls** - The most frequently used command in Linux to list directories
    
    Syntax: ls
    
2. **pwd** - Print working directory command in Linux
    
    <mark>Syntax: pwd</mark>
    
3. **cd** - Linux command to navigate through directories
    
    <mark>Syntax: cd [dir-name]</mark>
    
4. **mkdir** - Command used to create directories in Linux
    
    <mark>Syntax: mkdir [new-dir-name]</mark>
    
5. **rmdir -** Command used to permanently delete an empty directory
    
    <mark>Syntax: rmdir [dir-name]</mark>
    
6. **mv** - Move or rename files in Linux
    
    <mark>Syntax: mv [source] [destination]</mark>
    
7. **cp** - Similar usage as mv but for copying files in Linux
    
    **Syntax: cp &lt;source&gt; &lt;destination&gt;**
    
8. **rm** - Delete files or directories
    
    <mark>Syntax: rm [file/dir-name]</mark>
    
9. **touch** - Create blank/empty files
    
    <mark>Syntax: touch [new-file-name]</mark>
    
10. **ln** - Create symbolic links (shortcuts) to other files
    
    **<mark>Syntax: </mark>** <mark>ln [target-file] [link-name]</mark>
    
11. **cat** - Display file contents on the terminal
    
    <mark>Syntax: cat [file-name]</mark>
    
12. **clear** - Clear the terminal display
    
    <mark>Syntax: clear or keyboard key cnt+l</mark>
    
13. **echo** - Print any text that follows the command
    
    <mark>Syntax: echo "text"</mark>
    
14. **less** - Linux command to display paged outputs in the terminal
    
    <mark>Syntax: less [file-name]</mark>
    
15. **man** - Access manual pages for all Linux commands
    
    <mark>Syntax: man [command-name]</mark>
    
16. **uname** - Linux command to get basic information about the OS
    
    <mark>Syntax: uname</mark>
    
17. **whoami** - Get the active username
    
    <mark>Syntax: whoami</mark>
    
18. **tar** - Command to extract and compress files in Linux
    
    <mark>Syantx: tar [options] [archive-file]</mark>
    
19. **grep** - Search for a string within an output
    
    <mark>Syntax: grep [pattern] [file-name]</mark>
    
20. **head** - Return the specified number of lines from the top
    
    <mark>Syantx: head [file-name]</mark>
    
21. **tail** - Return the specified number of lines from the bottom
    
    <mark>Syantx: tail [file-name]</mark>
    
22. **diff** - Find the difference between two files
    
    <mark>Syantx: diff [file-name-1] [file-name-2]</mark>
    
23. **cmp** - Allows you to check if two files are identical
    
    <mark>Syantx: cmp [file-name-1] [file-name-2]</mark>
    
24. **comm** - Combines the functionality of diff and cmp
    
    <mark>Syantx: comm [file-name-1] [file-name-2]</mark>
    
25. **sort** - Linux command to sort the content of a file while outputting
    
    <mark>Syantx: sort [file-name]</mark>
    
26. **export** - is bash shell BUILTINS commands, which means it is part of the shell. It marks an **environment variables** to be exported to child processes.
    
    <mark>Syantx: export name[=value]</mark>
    
27. **zip** - To create a zip files in Linux
    
    <mark>Syntax: zip [options] zip file files_list</mark>
    
28. **unzip** - Unzip files in Linux
    
    <mark>Syntax: unzip [zip-file-name]</mark>
    
29. **ssh** - Secure Shell command used in Linux to connect remote server
    
    <mark>Syntax: ssh -i [key-name] user_name@host(IP/Domain_name)</mark>
    
30. **service** - Linux command to start and stop services
    
    <mark>Syntax: service [service-name] [start/stop/status/enable]</mark>
    
31. **ps** - Display active processes
    
    <mark>Syntax: ps</mark>
    
32. **kill and killall** - Kill active processes by process ID or name
    
    <mark>Syntax: ps [Process-ID/name]</mark>
    
33. **df** - Display disk filesystem information
    
    <mark>Syntax: Syntax: df</mark>
    
34. **mount** - Mount file systems in Linux
    
    <mark>Syntax: mount -t [type] [device dir]</mark>
    
35. **chmod** - Command to change file permissions
    
    <mark>Syantx: chmod [permissions] [file-name]</mark>
    
36. **chown** - Command for granting ownership of files or folders
    
    <mark>Syantx [chown owner_name] [file_name]</mark>
    
37. **ifconfig** - Display network interfaces and IP addresses
    
    <mark>Syantx ifconfig</mark>
    
38. **traceroute** - Trace all the network hops to reach the destination
    
    <mark>Syantx traceroute [route]</mark>
    
39. **wget/curl** - Direct download files from the internet
    
    <mark>Syantx: weget/curl [request-url]</mark>
    
40. **ufw** - Firewall command
    
    <mark>Syantx: ufw [allow] [port]</mark>
    
41. **iptables** - Base firewall for all other firewall utilities to interface with
    
42. **apt, pacman, yum, rpm** - Package managers depending on the distro
    
    <mark>Syntax: sudo apt/pacman/yum/rpm</mark>
    
43. **sudo** - Command to escalate privileges in Linux
    
    <mark>Syantx: sudo</mark>
    
44. **cal** - View a command-line calendar
    
    <mark>Syantx: cal</mark>
    
45. **alias -** Create custom shortcuts for your regularly used commands
    
    <mark>Syantx: alias [name]=[value]</mark>
    
46. **dd** - Majorly used for creating bootable USB sticks
    
47. **whereis** - Locate the binary, source, and manual pages for a command
    
    <mark>Syntax: whereis [file-name]</mark>
    
48. **whatis** - Find what a command is used for
    
    <mark>Syantx: whatis [command-name]</mark>
    
49. **top** - View active processes live with their system usage
    
    <mark>Syantx: top</mark>
    
50. **useradd and usermod** - Add a new user or change existing users data
    
    <mark>Syantx: sudo useradd [new-user-name]</mark>
    
    <mark>Syantx: sudo usermod [change-data]</mark>
    
51. **passwd** - Create or update passwords for existing users
    
    <mark>Syantx: sudo passwd [user-name]</mark>
    

### **Git And GitHub Commands:**

1. `git config:` It is used to set the name of the author and the email address which you want your commitment to addressing.
    
    <mark>Syntax: git config –global user.name “[user-name]”</mark>
    
    <mark>Syntax: git config –global user.email “[email address]”</mark>
    
2. `git init:` It is used to start a new git repository. This is generally used at the beginning.
    
    <mark>Syntax: git init [repo name]</mark>
    
3. `git clone:` This command is used to clone or copy a repository from a URL. This URL generally is a GitHub, bitbucket server, a stash, or any other version control and source code management repository holding service.
    
    <mark>Syntax: git clone [URL]</mark>
    
4. `git add:` It is used to add a file to the staging area. Instead of choosing a single file name, you can also choose to give all filenames with an \*.
    
    <mark>Syntax: git add (filename)</mark>
    
    <mark>Syntax: git add *</mark>
    
5. `git commit –m:` It is used to snapshot or record/save a file in its version history permanently.
    
    Giving a message text at the end of the commit command helps in identifying the details about the commit code.
    
    <mark>Syntax: git commit –m [type in a message]</mark>
    
6. `git commit –a:` This commit command is used to commit any such file which has been added as a result of the git add command. It is also responsible for committing any other files to which you have brought a change to since then.
    
    <mark>Syntax: git commit -a</mark>
    
7. `git diff:` As the name suggests, this command is used to display all the differences between the files until the changes have not yet been staged.
    
    <mark>Syntax: git git diff</mark>
    
8. `git diff –staged:` It is used to display all the differences between staging area files and the latest version, which might be present.
    
    <mark>Syntax: git diff -staged</mark>
    
9. `git diff [first branch] [second branch]:` This is a very effective command as it is used to display the differences present between the two branches.
    
    <mark>Syntax: git diff [first branch] [second branch]</mark>
    
10. `git diff [commit-id-1] [commit-id-2]:` This is a very effective command as it is used to display the differences present between the two commits.
    
    <mark>Syntax: git diff [commit-id-1] [commit-id-2]</mark>
    
11. `git reset [file]:` This command, as the name suggests, is used to unstage a file. Even though it unstages the file, still the contents of the file have stayed intact.
    
    <mark>Syntax: git reset [file]</mark>
    
12. `Git reset [commit]:` It is used to undo all the changes that have been incorporated as a part of a commit after a specified commit has taken place. This helps in saving the changes locally on the computer.
    
    <mark>Syntax: git reset [commit]</mark>
    
13. `Git reset –hard [commit]:` This command is used to discard all the history and takes us to the last specified commit.
    
    <mark>git reset –hard [commit]</mark>
    
14. **Git status:** This is one of the most frequently used as this is used to list down all the files which are ready to be committed.
    
    <mark>git status</mark>
    
15. `Git rm:` As in Unix, rm is used to remove; in the same way, rm is used to delete the file from the present working directory and is also used to stage the deletion process.
    
    <mark>Syntax: git rm [file]</mark>
    
16. `Git log:` This is used for listing down the version history for the current working branch.
    
    <mark>Syntax: git log</mark>
    
17. `Git log --online:` This is used for listing down the version history for the current working branch with short information.
    
    <mark>Syntax: git log</mark>
    
18. `git log –follow:` This is similar to that of git log with the additional difference that it lists the version history for a particular file, which often includes the renaming of the file also.
    
    <mark>Syntax: git log –follow [file]</mark>
    
19. `git show:` This is used to display the metadata and all the content related changes of a particular commit.
    
    <mark>Syntax: git show [commit]</mark>
    
20. `git tag:` This is used to give particular tags to the code commits.
    
    <mark>Syntax: git tag [commit-id]</mark>
    
21. `git branch:` Git branch command is used to list down all the branches that are locally present in the repository.
    
    <mark>Syntax: git branch</mark>
    
22. `Git branch [branch-name]:` This is used to create a new branch.
    
    <mark>Syntax: git branch [branch-name]</mark>
    
23. `git branch -d [branch name]` This command deletes the feature branch.
    
    <mark>Syntax: git branch -d [branch-name]</mark>
    
24. `git checkout` This command is used to switch from one branch to another.
    
    <mark>Syntax: git checkout [branch-name]</mark>
    
25. `git checkout -b [branch name]`This command creates a new branch and also switches to it.
    
    <mark>Syntax: git checkout -b [branch-name]</mark>
    
26. `git merge`
    
    `git merge [branch name]`This command merges the specified branch’s history into the current branch.
    
    <mark>Syntax: git merge [current-branch-name]</mark>
    
27. `git remote` This command is used to connect your local repository to the remote server.
    
    <mark>Syntax: git remote add [Remote Repo Link]</mark>
    
28. `git remote:` This git command lists all the remote connections of your local repository that you have with the other repositories.
    
    <mark>Syntax: git remote</mark>
    
29. `git push` This command sends the committed changes of the master branch to your remote repository.
    
    <mark>Syntax: git push [Repo-url] master</mark>
    
30. `git push –all [variable name]`This command pushes all branches to your remote repository.
    
    <mark>Syntax: git push [Repo-url]</mark>
    
31. `git push [variable name] :[branch name]`This command deletes a branch on your remote repository.
    
    <mark>Syntax: git push [Repo-url] [branch-name]</mark>
    
32. `git pull` This command fetches and merges changes on the remote server to your working directory.
    
    <mark>Syntax: git pull [Repo-url]</mark>
    
33. `git stash` This command temporarily stores all the modified tracked files.
    
    <mark>Syntax: git stash save</mark>
    
34. `git stash pop`This command restores the most recently stashed files.
    
    <mark>Syntax: git stash pop</mark>
    
35. `git stash[stash-id]`This command restores the specific stashed files.
    
    <mark>Syntax: git stash [stash-id]</mark>
    
36. `git stash list` This command lists all stashed changesets.
    
    <mark>Syantx: git stash list</mark>
    
37. `git stash drop`This command discards the most recently stashed changeset.
    
    <mark>Syantx: git stash drop</mark>
    

*Thank you for reading the article*

*Happy Learning!*

#linux #git #github #devops