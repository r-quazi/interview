##  Devops Interview questions | Devops Telephonic interview - 3 ( Mock Interview ) 

------------------------------------------


- Mock interview video - https://youtu.be/IrIF9IjOwgs
- Mock interview Answers - https://youtu.be/RtYw7f0KyV0?feature=shared


0. Can you just walk me throuh what are the tools you have worked on and the daily activities ?


-----------------------
-----------------------

# GIT
---------------------------------------------------------------------------------------------------------------------------------
1. What is git-cherry-pick? why we use it?
Ans :

```


Git Cherry-Pick Guide

Purpose: Apply specific commits from one branch to another without merging the entire branch.
Usage: Transfer individual changes, undo accidental commits on wrong branches, and revitalize lost commits from closed PRs.

Common Scenarios:

Undoing Changes:
- Wrong Branch Commits: Switch to the correct branch and use git cherry-pick <commit-hash> to apply the commit.

Backporting Fixes:
- Apply bug fixes to older branches selectively with git cherry-pick.

Splitting Commits:
- For commits with multiple changes, cherry-pick allows splitting into smaller commits.

Reordering Commits:
- Change commit order or move between branches with cherry-pick.

Example Workflow:

Fixing Bugs Quickly:
1. Bug identified during new feature development.
2. Create a commit for the bug fix.
3. Cherry-pick the commit to the main branch: git cherry-pick <commit-hash>

Steps to Cherry-Pick:

1. Ensure you're on the target branch where the commit should be applied.
2. Run git cherry-pick <commit-hash> for a single commit.
   - For multiple commits, list all commit hashes.
3. Resolve any conflicts that occur.
4. Continue with git cherry-pick --continue or abort with git cherry-pick --abort.

Caveats:

- Commit Duplication: Be cautious as cherry-picking can duplicate commits.
- Merge Histories: Overuse can complicate merge histories.

Remember: While cherry-pick is powerful, prefer merging over cherry-picking when dealing with multiple commits to maintain a clean history.

```


Git cherry pick is used to apply specific commits from one branch to another , we can pick individual commits and apply them to your current workingbranch  without merging the entire branch  . we can selected specific changes from branch and cherry pick them into another branch.

git cherry-pick can be useful for undoing changes. For example, say a commit is accidently made to the wrong branch. You can switch to the correct branch and cherry-pick the commit to where it should belong.

other use cases : 

Sometimes a feature branch may go stale and not get merged into main. Sometimes a pull request might get closed without merging. Git never loses those commits and through commands like git log and git reflog they can be found and cherry picked back to life.

Backporting fixes: If you have a bug fix in one branch and you want to apply it to an older or different branch without merging the entire branch, you can use git cherry-pick to selectively apply the fix.

Splitting commits: You might have a commit that contains multiple changes, and you want to apply only a subset of those changes to another branch. Cherry-picking allows you to split a commit into smaller, more focused commits* * * *   Reordering commits: If you want to change the order of commits in your branch's history or move commits between branches, you can use git cherry-pick to achieve this.


When a bug is discovered it is important to deliver a fix to end users as quickly as possible. For an example scenario,say a developer has started work on a new feature. During that new feature development they identify a pre-existing bug. The developer creates an explicit commit patching this bug. This new patch commit can be cherry-picked directly to the main branch to fix the bug before it effects more users.


With the cherry-pick command, Git lets you incorporate selected individual commits from any branch into your current Git HEAD branch. When performing a git merge or git rebase , all the commits from a branch are combined.
It's also possible to cherry-pick multiple commits but merge is the preferred way over cherry-picking.


First, make sure you are on the branch where you want to apply the selected commit(s).

Run the git cherry-pick command followed by the commit hash of the commit you want to apply. For example:

`git cherry-pick <commit-hash>`

You can specify multiple commit hashes in a single command to apply multiple commits in sequence

Git will attempt to apply the changes made by the selected commit(s) to your current branch. If there are any conflicts (i.e., changes in the selected commit(s) conflict with changes in your current branch), Git will pause the process and prompt you to resolve the conflicts manually


After resolving any conflicts, you can continue the cherry-pick process by running git cherry-pick --continue. If you decide to abort the cherry-pick, you can use git cherry-pick --abor 


the crrypick is useful however   it can lead to commit duplication and complex merge histories if not used judiciously.

    




----
----

2. Let’s say you’re working on new feature in some branch, now your manager says stop working on that and change few other things on old code. Here after changing the old code, I need to work on new code, so I need to place my new changes some place How would handle this scenario?


- Ans :

```
- git stash save "sdf"
-  git checkout ol-branch
-  git commit -m "maonf"
-  git chekout stashed-branch
-  git stash apply

for local only -- trmporary private commit
not pushed on internet for officepc -> homepc no access


```
In this case we can use the git stash , Stashing is a handy way to temporarily save your changes while you work on something else, and it helps you avoid cluttering your commit history with incomplete work.


We need to first save the changes use ` git stash save "Working on new feature"   `  
then Checkout the Branch for Old Code: `git checkout old-code-branch`
Make and Commit Changes: `git commit -m "Made changes to old code"`
Switch Back to the New Feature Branch:   `git checkout new-feature-branch`
Apply Stashed Changes: `git stash apply`
Resolve Any Conflicts:


Stash command is for local hide your changes.
If you want work remotely you must commit and push. for example i am doing work in hybrid mode in office i made some changes to file and stashed and pushed to main repo then on home on my laptop i pulled the repo , then the repo will not have stashed changes. in such cases we need either a branch for stash or better go with some commits.

 you can look at stash as a temporary "private" commit. However the strategy depends on developers that s just a matter of taste.
 
 the git stash save command is deprecated, which means that any new development should only use push.
 






-------
------
3. What is a conflict in git? have you worked on it ?

- Ans :

```
- conflict may arise when... git cant determine wrong /correct
- only affects dev conducting merge other unaware
- merging will halt unless conflict resolved
- dev responsibility to resolve conflict
-  easy ib git as comp. to svn 
-  can use git status to get the detail about conflict shows modified file and commit , flags
-  file identified , update code then merge
-  git diff helpful , <<< ===>>>
-  can avoid conflict using git fetch , communication , seperate branches 



```

The conflicts may arise when two  people have changed the same lines in a file, or if one developer deleted a file while another developer was modifying it.In these cases, Git cannot automatically determine what is correct. Conflicts only affect the developer conducting the merge, the rest of the team is unaware of the conflict. Git will mark the file as being conflicted and halt the merging process. It is then the developers' responsibility to resolve the conflict.

In SVN resolving conflicts is hardand time consuming in git it can be resolved quickly via git conflict tools whenver we merge a branch or a file cmmitted.


We can use git status to find the details about conflicts  it will show which file is mofidfied and related commits , we can provide flags or options to get more detailes.

once the file is identified we can edit the file make some changes and commit then we can merge it.

git diff helps find differences between states of a repository/files. This is useful in predicting and preventing merge conflicts.

else we can resolve the configs from the GitHUb as well.  git displayes <<< === >>> less than equal and greater than symbols where conflicts it detects in file.


We can avoid the conflicts using git fetch , git pull ,  communication within the team , seperate branches for different environments.



--------
--------


4. command to list all branches in a repo?

There are three commands to list all branches in a Git repository:
```
git branch: This command lists all local branches.
git branch -r: This command lists all remote branches.
git branch -a: This command lists all local and remote branches.
git show-branch: Provides a detailed view of branch relationships and commit history.
git branch --list: Lists all local branches.
git for-each-ref --format="%(refname:short) %(objectname) %(subject)" refs/heads/: Lists local branches with commit hashes and commit subjects.



```
    





-----------------
-----------------------
-----------------------


# Maven
--------------------------------------------------------------------------------------------------------------------------
5. .m2 is local repository for maven, now I don’t want to use .m2 folder as my local repository I want to use some other folder as my local, is it possible in maven? If yes, how would you do that?

```
mvn install -Dmaven.repo.local=/alternate/repo/location 
```
6. maven follows convention over configuration that means it assumes code should be there under src/main/java, test cases under src/tests and many more.Here my requirement is I don’t want to follow that conventions I need to use different folder structure is that possible in maven?
```
mvn help:effective-pom -Doutput=pom_eff.xml
```
7. What are dependency and plugin in maven? Give one example for each?
8. What are 3 build life cycles in maven?
9. In Which tag we will mention output artifact type( like jar, war or any other)?



-----------------------
-----------------------
-----------------------


# Unix and Shell scripting 
---------------------------------------------------------------------------------------------------------------------
10. In a file I have ip addresses , I want list unique ip addresses with number of times its present in file?
```
grep -E -o "([0-9]{1,3}[\.]){3}[0-9]{1,3}" logfile | sort | uniq -c | sort -nr
```


--------------------------------

11. What is exit status in UNIX?

ANS :

In UNIX-like operating systems, including Linux, the exit status, or exit code, is a numeric value returned by a process when it terminates. The exit status is a way for a process to communicate the result of its execution to the calling process or the system.

Here are key points about exit status in UNIX:


Exit Status Values:

    0: Successful execution
    1-255: Indicates an error or specific failure condition
    126: Command invoked cannot execute
    127: "command not found"
    128: Invalid argument to exit
    128+n: Fatal error signal "n"


    
1. **Numeric Value:**
   - The exit status is a numeric value in the range of 0 to 255.
   - A status of 0 typically indicates successful completion, while non-zero values indicate an error or some form of abnormal termination.

2. **Zero Exit Status (Success):**
   - A process conventionally returns an exit status of 0 to indicate successful execution.
   - This is often used as a signal that the process completed its task without encountering errors.

3. **Non-Zero Exit Status (Error):**
   - Non-zero exit statuses are used to indicate various error conditions or failures.
   - Different non-zero values may have specific meanings, depending on the program or script.

4. **Checking Exit Status:**
   - In shell scripts or command-line operations, the exit status of the last command or process can be checked using the `$?` variable.
   - For example:
     ```bash
     command_that_may_fail
     if [ $? -eq 0 ]; then
       echo "Command succeeded."
     else
       echo "Command failed."
     fi
     ```

5. **Error Codes Convention:**
   - While the specific meaning of non-zero exit codes can vary, there are some conventions. For example, a process might use different non-zero values to indicate specific types of errors or failure conditions.

6. **Exit Status in Shell Scripts:**
   - In shell scripts, the `exit` command is used to set the exit status explicitly. For example:
     ```bash
     # Exit with success status
     exit 0

     # Exit with an error status
     exit 1
     ```

7. **Propagation:**
   - When a process exits, its exit status is typically propagated to the parent process, allowing the parent to determine the outcome of the child process's execution.

Understanding and properly handling exit status is crucial in scripting and automation to ensure appropriate actions are taken based on the success or failure of executed commands or processes.


---------------------

12. Lets say I have shell script name magic.sh when I execute. It gives “This is from magic.sh”, so now if I change file name to magic-test.sh I should get “This is from magic-test.sh” basically as name of file chages my output should also change?


ANS :

Certainly! You can achieve this by dynamically determining the script's own filename within the script and using it to customize the output. Here's an example using a common technique in shell scripts:

```bash
#!/bin/bash

# Get the base name of the script
script_name=$(basename "$0")

# Customize the output based on the script name
if [ "$script_name" = "magic.sh" ]; then
    echo "This is from magic.sh"
elif [ "$script_name" = "magic-test.sh" ]; then
    echo "This is from magic-test.sh"
else
    echo "Unknown script name: $script_name"
fi
```

In this script:

- `basename "$0"` extracts the base name of the script from the path, which includes the filename.
- The script then uses an `if` statement to check the script name and customize the output accordingly.

When you execute `magic.sh`, it will print "This is from magic.sh," and if you change the filename to `magic-test.sh` and execute it, you'll get "This is from magic-test.sh." This way, the script dynamically adapts its behavior based on its own filename.

---------------------

13. What is shebang ? Why it is used?

ANS :

A shebang, also known as a hashbang or pound-bang, is the character sequence "#!" that appears at the beginning of a script or an executable file in Unix-like operating systems. It is followed by the path to the interpreter that should be used to execute the script.

For example:
```bash
#!/bin/bash
```

In this example, the shebang line indicates that the script should be executed using the Bash shell.

Key points about shebang:

1. **Interpreter Specification:**
   - The shebang line specifies the interpreter that should be used to execute the script or program.
   - It is placed at the very beginning of the file, preceded by the "#" (hash) character.

2. **Execution Environment:**
   - The shebang informs the system about the interpreter or command that should be used to run the script.
   - It defines the execution environment for the script.

3. **Script Portability:**
   - The shebang allows scripts to be written in various scripting or programming languages, making the scripts more portable across different systems.
   - For example, a script written in Python might start with `#!/usr/bin/env python`, and a Bash script with `#!/bin/bash`.

4. **Multiple Commands:**
   - The shebang can also be used to specify multiple commands or options for the interpreter.
   - For example, `#!/bin/bash -e` would start the Bash shell with the `-e` option, which exits the script if any command it runs exits with a non-zero status.

5. **Default Interpreter:**
   - If no shebang is present, the system typically uses a default interpreter to execute the script (often `/bin/sh`).

6. **Shebang Examples:**
   - Bash script: `#!/bin/bash`
   - Python script: `#!/usr/bin/env python`
   - Perl script: `#!/usr/bin/perl`

In summary, the shebang is used to specify the interpreter for executing a script or program. It is essential for defining the scripting or programming language, ensuring the correct execution environment, and enhancing the portability of scripts across different systems.


---------------------



-----------------------
-----------------------
-----------------------

# Jenkins 
--------------------------------------------------------------------------------------------------------
14. How to Downgrade plugins in Jenkins?
15. Have you worked on Jenkinsfile? Can we use different nodes for each stage?
16. Can you list few ways by which we can trigger our build in Jenkins? What is the difference between Build Periodically and Poll SCM? 




-----------------------
-----------------------
-----------------------

# AWS
-------------------------------------------------------------------------------------------------------------
17. What are roles and policies in AWS IAM?
18. Lets say I have 50 users , for all 50 users I need to provide same privileges how do it? 
19. I want to give programmatic access means They can access AWS services via api’s  But should not be access AWS web console
20. As AMI is region specific I want create Machine with AMI which there in other Region is that possible?
21. Why we need security groups? By default what is outbound rules?
22. What is VPC? Give a brief about VPC? 
23. Have you worked on Load balancers? If Yes, tell which load balancers you have used?
24. Lets say I have created auto scaling rule when ever Load goes more than 60% create a new instance Currently I have 3 machines, 1st machine load  is 62% , 2nd machine 30% and 3rd also 30%.  Now will auto scale rule creates new machine ?




-----------------------
-----------------------
-----------------------

# Ansible
-----------------------------------------------------------------------------------------------------------------------
25. What is the best method to make your ansible YAML files reusable? have you created roles ?
26. What is ansible vault and ansible tower?
27. Lets say I have playbook need to be run with Root user how would you do this?
28. Difference between copy and fetch module?

Docker
------------------------------------------------------------------------------------------------------------------------------
29. Lets say I have 1 GB file that has to be sent to docker daemon, as its 1GB it will take muchtime and network too. By which option while building dockerfile we can send the fileIn better manner?
30. What is the difference between ADD and COPY docker instructions in Dockerfile?
31. Command to remove to stopped and running Containers?
32. Inside the container I did many changes like  Creating, modifying and deleting file but I Wanted to check which files has been changed And what action has been taken what is the  Command we need to use ?


Kubernetes
--------------------------------------------------------------------------------------------------------------------------------------
33. List objects you know in kubernetes?Give a brief about each object?
34. Command to list pods and deployments
