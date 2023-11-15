##  Devops Interview questions | Devops Telephonic interview - 4 ( Mock Interview ) 
https://www.youtube.com/watch?v=GhFYJOD4By4&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=4

-----------------------------------------------

0. Tell me about yourself and what project and tools have you used ?

GIT
---------------
1. What is git reset ? Types of reset ?
Ans :


Git reset is used to undo changes to your Git repository. It can be used to reset the HEAD Pointer, the index, or working directory  or it can be the combination of these three.

it  operates in a similar manner like git checout however the difference is pointer here , if abc is our main and Head and we checkout to xyz it will be branch xyz and main abc , but what git reset does is it checkout to branch xyz also makes it main .

Comparatively, git reset, moves both the HEAD and branch refs to the specified commit.

If git revert is a “safe” way to undo changes, you can think of git reset as the dangerous method. There is a real risk of losing work with git reset. Git reset will never delete a commit, however, commits can become 'orphaned' which means there is no direct path from a ref to access them. These orphaned commits can usually be found and restored using git reflog. Git will permanently delete any orphaned commits after it runs the internal garbage collector. By default, Git is configured to run the garbage collector every 30 days. Commit History is one of the 'three git trees' the other two, Staging Index and Working Directory are not as permanent as Commits. Care must be taken when using this tool, as it’s one of the only Git commands that have the potential to lose your work.

Whereas reverting is designed to safely undo a public commit, git reset is designed to undo local changes to the Staging Index and Working Directory. Because of their distinct goals, the two commands are implemented differently: resetting completely removes a changeset, whereas reverting maintains the original changeset and uses a new commit to apply the undo.




also git reset  can update the trees i.e  working directory , staging and commit.


The types of or options/falgs we use with git reset are --hard , --soft , --mixed


--hard can be very dangereous and destructive if we dont used carefully,   The Commit History ref pointers are updated to the specified commit. Then, the Staging Index and Working Directory are reset to match that of the specified commit. Any previously pending changes to the Staging Index and the Working Directory gets reset to match the state of the Commit Tree. This means any pending work that was hanging out in the Staging Index and Working Directory will be lost.

--mixed is the default operation mode. The ref pointers are updated. The Staging Index is reset to the state of the specified commit. Any changes that have been undone from the Staging Index are moved to the Working Directory.

--soft , the ref pointers are updated and the reset stops there. The Staging Index and the Working Directory are left untouched.

Example: git reset --hard HEAD~1 will move the branch pointer one commit back and discard all changes made in the last commit.


-------
------


2. How to delete local branch  and remote branch in git ?

Delete a Local Branch:

To delete a local branch, you can use the git branch command with the -d or -D option, followed by the branch name:

The -d option stands for "delete" and is used for a safe deletion. It will prevent deletion if the branch contains changes that are not yet merged. ( can als use -f for force delete )

The -D option stands for "force delete" and is used to forcefully delete the branch, regardless of whether it contains unmerged changes. Use this option with caution, as it can lead to data loss. 
```
# Safe delete (checks for unmerged changes)
git branch -d branch_name

# Force delete (does not check for unmerged changes)
git branch -D branch_name

```
Delete a Remote Branch:

To delete a remote branch, you can use the git push command with the --delete (or -d) option followed by the remote repository name and the branch name. Here's the command:
`git push origin --delete branch_name`
`git push origin --delete my_feature`


 If you are not sure whether or not a branch has been merged or has uncommitted changes, you can use the  command `git branch -v` to get more information about the branch:

    


-------
------

3. Difference between git diff and git status ?


`git diff` and `git status` are two Git commands that serve different purposes when it comes to managing and understanding changes in your Git repository:  git status only tells you the state of your file changes, git diff tells you the exact changes, 

1. **`git diff`**:
   - `git diff` is used to show the differences between two sets of changes in your Git repository.
   - It is typically used to compare the changes between:
     - The working directory and the staging area (index), which is achieved by running `git diff`.
     - Two different commits, branches, or tags. For example, `git diff commit1 commit2` will show the differences between two specific commits.
   - `git diff` provides a detailed view of what has changed in terms of code additions, deletions, and modifications. It can be very useful for reviewing and understanding the specifics of code changes.
   - It is a command for comparing actual file contents.

   Example:
   ```bash
   git diff          # Shows changes between working directory and index (staging area)
   git diff HEAD     # Shows changes between working directory and the latest commit
   git diff commit1 commit2  # Shows changes between two specific commits
   ```

2. **`git status`**:
   - `git status` is used to provide a high-level overview of the current state of your Git repository.
   - It displays information about:
     - Modified files in your working directory that are not yet staged for commit (in red).
     - Files that are staged and ready to be committed (in green).
     - Untracked files (files that Git is not currently tracking).
     - The current branch and whether it's ahead, behind, or up to date with the remote branch.
   - It does not show the specific line-by-line changes but rather provides a summary of the status of files in your repository.
   - `git status` is useful for quickly checking what you need to do next, such as committing changes, adding untracked files, or pushing to a remote repository.

   Example:
   ```bash
   git status
   ```

In summary, `git diff` is used for inspecting the actual changes in code or content, while `git status` is used for getting a broad overview of the state of your working directory and the staging area. They complement each other and are often used together to manage and review changes in a Git repository effectively.



-------
------

4. What are hooks in git?


Git hooks are scripts that are automatically executed when certain events occur in a Git repository. They can be used to automate tasks, enforce rules, and validate changes before they are committed or pushed to a remote repository.

There are two types of Git hooks: client-side and server-side.

    Client-side hooks are executed on the local machine of the user who is interacting with the repository.
    Server-side hooks are executed on the remote server where the repository is hosted.

Git hooks are stored in the .git/hooks directory of a repository. Each hook is a shell script, and its name corresponds to the event that triggers it. For example, the pre-commit hook is executed before a commit is made, and the post-push hook is executed after a commit is pushed to a remote repository.

Git hooks can be used for a variety of purposes, such as:

    Enforcing code formatting
    Running tests
    Validating commit messages
    Preventing commits to certain branches
    Generating documentation
    Notifying team members of changes

Git hooks are a powerful tool that can be used to automate and improve your development workflow.

Here are some examples of how Git hooks can be used:

    A pre-commit hook can be used to automatically format code before it is committed. This can help to ensure that all code in the repository is consistent in style.
    A post-commit hook can be used to run tests to ensure that the code is still working properly after the changes have been committed. This can help to prevent bugs from being introduced into the repository.
    A pre-push hook can be used to prevent commits to certain branches, such as the master branch. This can help to prevent accidental changes from being pushed to production.
    A post-push hook can be used to generate documentation for the code that has been pushed to the remote repository. This can help to keep the documentation up-to-date and make it easier for other developers to understand the code.

To create a Git hook, simply create a new file in the .git/hooks directory and name it after the event that you want it to trigger. For example, to create a pre-commit hook, you would create a new file called pre-commit.

Once you have created the hook file, you need to make it executable. To do this, run the following command:

chmod +x .git/hooks/pre-commit

You can now test the hook by committing some changes to the repository. If the hook works properly, you will see a message from the hook.

Git hooks can be a powerful tool for automating and improving your development workflow. If you are not already using them, I encourage you to check them out.


Hooks doesnt only mean sending some json payload like setting github webooks for jenkins the commands that we run git commit, git rebase etc also hooks which runs scripts in the  background.

Git hooks are scripts that are run at specific points in the Git workflow, such as before a commit is made, after a push is received, or after a branch is merged. They can be used to enforce policies, automate tasks, or simply notify you of events.

Webhooks are a way for two web applications to communicate with each other. When a webhook is triggered, a POST request is sent to a specified URL with a payload containing information about the event. This allows you to automate tasks in one application based on events in another application.





-------
------



MAVEN
--------
5. What are things you need to set, if you want download dependency from private repository ?
6. What are the issues you faced while working on maven projects?
7. Command to skip the test cases in maven.

JENKINS
----------
8. How to set Jenkins build to fail based specific word in console output ?
9. How to set Jenkins build to fail based specific word in console output ?
10. What are active and reactive parameters (Dynamic parameterization) in Jenkins ?
11. How to customize the build number display to something else in Jenkins job page?
12. What are multi branch pipeline?
13. What is shared library in Jenkins ?

UNIX & SHELL SCRIPTING
-----------
14. Command to find empty files in a given directory?
15. Commands you will use it for configuring ssh connectivity between 2 machines and what files will be present in .ssh folder?
16. How to schedule a shell script in unix machines?
17. Command to get load average ?
18. Need to identify ip addresses in log file and count of ip addresses in log file?

ANSIBLE
------------
19. Why ansible ? What makes ansible powerful than other tools like chef and puppet?
20. 5 modules that you have worked on? Can we create custom module ?
21. What is dynamic inventory in ansible?
22. Lets say I have both Ubuntu and centos machines as nodes I want install application tree using same playbook, how would you approach this scenario? 
23. How to handle prompts with ansible playbook?

DOCKER
----------
24. What does ONBUILD instruction do in Dockerfile?
25. What is the use of .dockerignore file?
26. I have dockerfile that accepts arguments, if I supply value as “1” then it should use maven 2.x version for base image and if I supply “2” then it should take maven latest as base image 
27. What are docker compose and docker swarm?

KUBERNETES
---------
28. Components in kubernetes architecture?
29. What are stateful sets in kuberentes?
30. Command to find which container has failed in pod and command to get logs of container 
31. Tools to maintain kubernetes log files 

AWS
-----
32. Services used AWS and tasks performed in AWS
