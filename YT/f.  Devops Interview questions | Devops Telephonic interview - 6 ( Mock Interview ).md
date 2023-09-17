##  Devops Interview questions | Devops Telephonic interview - 6 ( Mock Interview ) 
https://www.youtube.com/watch?v=Z_bbozP6ZW4&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=6

-------------------------------------------------------

1. What are the tools you have used and please elaborate your day to day activities ?




2. What is Continous integration Continous delivery and Continous deployment ?

## GIT :


3. which version of git you used ?

I use the latest version of Git, which is 3.1.1 as of September 17, 2023. I use the latest version of Git because it is the most stable and has the most features. I also use the latest version of Git to ensure that I am compatible with the other developers and tools that I use.

Here are some of the benefits of using the latest version of Git:

Stability: The latest version of Git has been tested and fixed to remove any known bugs.
Features: The latest version of Git includes the newest features and improvements.
Compatibility: The latest version of Git is compatible with the other developers and tools that you are using. I recommend that you also use the latest version of Git to get the most out of this powerful version control system.

"I have experience using various versions of Git, but I primarily use the latest stable version available at the time of my projects.

`$ git --version` to check version
`git update` to update git

shoudl go through update guide or porting guide before updateing version as they may release some nre featearure , deprecate some , may change fqcn   etc





---------
---------

4. what is git merge and git rebase ?

Git Merge lets you merge different Git branches. Git Rebase allows you to integrate the changes from one branch into another.


`git merge` and `git rebase` are two different methods in Git used to integrate changes from one branch into another. They have distinct approaches to combining branch histories, and each has its advantages and use cases:

**1. `git merge`:**
   - `git merge` is a command used to combine the changes from one branch into another branch, typically the current branch.
   - When you merge a branch, Git creates a new "merge commit" that has two parent commits: one from the current branch and one from the branch being merged.
   - This creates a linear history in the target branch, preserving the complete history of both branches. Merged branches maintain their original commit history.
   - Merging is often used for incorporating feature branches or topic branches into a main development branch (e.g., `master`).

   Usage:
   ```bash
   # Merge a branch into the current branch
   git merge branch_name
   ```

**2. `git rebase`:**
   - `git rebase` is a command used to incorporate changes from one branch into another by moving or reapplying commits from the source branch onto the tip of the target branch.
   - It effectively rewrites the commit history of the source branch, creating a linear sequence of commits in the target branch without merge commits.
   - This results in a cleaner and more linear history but may alter commit timestamps and commit hashes, which can be a concern in shared or collaborative workflows.
   - Rebasing is often used to keep feature branches or topic branches up to date with changes in the main development branch, resulting in a more streamlined commit history.

   Usage:
   ```bash
   # Rebasing a branch onto another branch
   git checkout feature_branch
   git rebase target_branch
   ```

**Key Considerations:**
- Use `git merge` when you want to preserve the original branch's commit history and create a merge commit to signify the merge.
- Use `git rebase` when you want a linear and cleaner commit history but are willing to rewrite commit history.
- Be cautious with rebasing if you're working in a shared repository, as it can create complications when multiple people are collaborating on the same branch.

In summary, `git merge` is suitable for integrating branches with their full commit history, while `git rebase` is used to create a more linear and streamlined commit history but involves rewriting commits. The choice between these two methods depends on your project's requirements and your preference for commit history presentation.






---------
---------

5. Do you know git squash ?

Yes, I'm familiar with the concept of "squashing" commits in Git. Squashing is a technique used to combine multiple commits into a single, more meaningful commit. This can help keep your commit history cleaner and more organized, especially before merging a feature branch into a main branch. Squashing is typically done using an interactive rebase.

Here's how you can squash commits using an interactive rebase:

1. First, make sure you are on the branch that you want to squash commits in. For example:

   ```bash
   git checkout feature_branch
   ```

2. Start an interactive rebase for the last N commits you want to squash, where N is the number of commits you want to combine plus one. For example, to squash the last three commits, you would run:

   ```bash
   git rebase -i HEAD~3
   ```

   This will open an editor with a list of commits in reverse chronological order.

3. In the rebase interactive editor, change the word "pick" to "squash" (or just "s" for short) for the commits you want to squash. Keep "pick" for the commit you want to keep as the final, combined commit. For example:

   ```plaintext
   pick abc123 Some meaningful commit message
   squash def456 Another commit message
   squash 789xyz Yet another commit message
   ```

4. Save and close the editor.

5. Git will then prompt you to edit the commit message for the combined commit. You can modify the commit message to create a meaningful summary of the changes.

6. Save and close the commit message editor.

7. Git will complete the rebase process and create a single squashed commit with the changes from the selected commits.

8. If you had pushed the branch to a remote repository before squashing, you may need to force push the branch to update the remote branch's history. Be cautious when force pushing, especially in shared repositories.

Squashing commits can make your commit history more concise and easier to understand, particularly when you have made several incremental commits during development. It's a useful practice before merging feature branches into the main branch or for creating cleaner, more organized commit histories for your projects.

-----------------------------------
| Git Squash	     |    Git Rebase | 
------------------------------------
| You can combine multiple commits into a single commit.	     |    	Applies commits on top of the different base commits. | 
| After using git squash your commit history will be more clean and organized.		     |    You can form a new branch by using previous commits.  |
| Must be done on private branches. 		     |    Rebasing can be done on a feature branch or shared branch. |
| By using squishing you can maintain clean and logical commit history.	     |    	By using rebase command you can keep your branch up to date. |

|--------------------- |---------------------------|



---------
---------

6. What branching strategy you used and which is good ?










---------
---------

========

7. Have you worked on build tool maven ?
8. Please explain 3 maven build phase in details ?
9. If i dont want to use .m2 how to configure that ?
10. If you want to use mvn deploy what are the settings you want to do ?
11. What is GA Base ?   ///// group id , artifcat id and version
12. what is the packaging value if you dont define in pom.xml ?
13. what are the all job types of jobs you have worked on ?
14. Can we have a job for PR ?
15. When the merge is done how the branch can be deleted automatically ?
16. What is the use of Post section in pipeline ?
17. How can we taked the continous backup in  jenkins ?

18. Docker version you are using ?
19. Have you worked on docker compose and docker swarm ?
20. Have you worked on docker volume and bind mount ? why it is needed ?
21. Why we use dockerignore ?
22. Is it possible to name dockerfile as myproject.txt ?
23. how to remove all stopped containers and images ?

24. Are you administring k8 or deploying ?
25. Can we deploy pods on master node ?
26. Have you come across configmap and why we use it ?
27. What is default deployment strategy in k8 ?
28. Have you used helm and why we need helm ?
29. how can we find the unised values in helm ?
30. have you come across exit status, why we use that exit status ?
31. command to find the os of system ?

32. in ansible if we have to run few command on centos and linus how to do that >
33. ansible galaxy ? why we use ?
34. simple example of adhoc command ?
35. how to store the output of command ?
36. what are handlers in ansible and why we use it ?

37. what are the aws services you have worked on ?  
