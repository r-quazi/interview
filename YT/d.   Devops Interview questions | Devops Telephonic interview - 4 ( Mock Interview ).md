##  Devops Interview questions | Devops Telephonic interview - 4 ( Mock Interview ) 
https://www.youtube.com/watch?v=GhFYJOD4By4&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=4

-----------------------------------------------

0. Tell me about yourself and what project and tools have you used ?

GIT
---------------
1. What is git reset ? Types of reset ?
Ans :

```
Git Reset :
 -  undo changes
 -  reset HEAD pointer
 - index
 - working directory
 - combination of these

Git checkout vs Git Resest :
 - git reset does is it checkout to branch xyz also makes it main .
 - git reset, moves both the HEAD and branch refs to the specified commit.

-  Git revert is safer than git reset
 - Never delete commit however it will orphaned ( no ref) but can be restored using git reflog 


Type of reset :
  -  --hard : very danger , destructive any pending work that was hanging out in the Staging Index and Working Directory will be lost.
  -  --soft ;  ref pointers are updated , reset stops there. Staging Index , Working Directory  untouched.
  - -- mixed  : default operation mode. The ref pointers are updated. The Staging Index is reset to the state of the specified commit. Any changes that have been undone from the Staging Index are moved to the Working Directory.

Example: git reset --hard HEAD~1 will move the branch pointer one commit back and discard all changes made in the last commit.


```

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

```
Local Branch :

-d or -D 
-d : safe delete , It will prevent deletion if the branch contains changes that are not yet merged. ( can als use -f for force delete )

- D : force delete , forcefully delete the branch, regardless of whether it contains unmerged changes.

Remote Branch :
`git push origin --delete branch_name`
to check unmerge branch r uncommited changes we can do : git branch -v
```


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

```
- managing and understanding changes
Git diff :
 - show difference
 - compare changes
    -  between stating and working dir i.e git diff
    -  between diff commits   branches/tags : git diff commit1 commit2
  - provide detailed view of changes <<<===>>> , + , -
  - git diff HEAD :  changes between working directory and the latest commit

Git Status :
  -  High level overview of current state of repo.
  -  Info about :
      -  modified files
      - uncommitted files / untracked files
      - current branch and ahead /behind commits
  -  useful for quickly checking what need to do next   








```

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

```
Git Hooks :
  - Scripts that auto trigger when event happen
  - used to automate tasks , enforce rules,
  - validate changes b4 commit
  - preventing commit to certain branches
  - generating documentation
  - notifying members
  - 2 types : 
	  - Client Side : executed on local machine
	  - Server side : executed on remote  server

- Hooks are stored i .git/hooks
-  each hook is shell script name is same as event it triggers
Steps to create Hook :
- create file in .git/hooks
- name pre-commit , post-commit 
- add whatever script you want
- chmod +x

-- Git Hooks (script on local machine) and Git webhooks ( two application) both are different.

Example :
pre-commit: auto format the code
post-commit: run tests
pre-push: prevent commit on certain branches
post-push:generate documentation
```

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





-----------------
-------------------
------------------


# MAVEN
--------
5. What are things you need to set, if you want download dependency from private repository ?
6. What are the issues you faced while working on maven projects?
7. Command to skip the test cases in maven.



-----------------
-------------------
------------------


# JENKINS
----------

9. How to set Jenkins build to fail based specific word in console output ?

Ans :

In Jenkins, you can set a build to fail based on specific words in the console output using the "Text Finder" or "Text Finder (Simple)" plugin. Here's a step-by-step guide on how to achieve this:

**Using Text Finder Plugin:**

1. **Install the Text Finder Plugin:**
   - Navigate to "Manage Jenkins" -> "Manage Plugins" -> "Available" tab.
   - Search for "Text Finder" or "Text Finder (Simple)" in the list.
   - Select the checkbox next to the plugin and click "Install without restart."

2. **Configure the Text Finder in Your Jenkins Job:**
   - Open or create the Jenkins job for which you want to set the build to fail based on specific words.
   - In the job configuration, scroll down to the "Post-build Actions" section.
   - Click on "Add post-build action" and select "Fail the build if...".

3. **Define the Text Finder Criteria:**
   - In the "Text Finder" section, you can configure the criteria for which the build should fail.
   - Enter the specific words or regular expressions you want to search for in the console output.
   - Specify other parameters like case sensitivity, match build log, etc.

4. **Save and Run the Job:**
   - Save the job configuration.
   - Run the job, and it will now fail if the specified words are found in the console output.

**Using Text Finder (Simple) Plugin:**

1. **Install the Text Finder (Simple) Plugin:**
   - Follow the same steps as mentioned above to install the "Text Finder (Simple)" plugin.

2. **Configure the Text Finder (Simple) in Your Jenkins Job:**
   - Open or create the Jenkins job for which you want to set the build to fail based on specific words.
   - In the job configuration, scroll down to the "Post-build Actions" section.
   - Click on "Add post-build action" and select "Fail the build if...".

3. **Define the Text Finder (Simple) Criteria:**
   - In the "Text Finder (Simple)" section, you can configure the criteria for which the build should fail.
   - Enter the specific words or regular expressions you want to search for in the console output.
   - Specify other parameters like case sensitivity, match build log, etc.

4. **Save and Run the Job:**
   - Save the job configuration.
   - Run the job, and it will now fail if the specified words are found in the console output.

By using either the "Text Finder" or "Text Finder (Simple)" plugin, you can easily set up Jenkins to fail a build if specific words or patterns are detected in the console output, helping you catch issues early in the build process.


Or : 

To set a Jenkins build to fail based on a specific word in the console output, you can use the Groovy scripting plugin. This plugin allows you to execute Groovy scripts in your Jenkins pipeline.

Here is an example of a Groovy script that will fail a Jenkins build if the word "ERROR" is found in the console output:
Groovy

import hudson.model.*

def logManager = manager.getLogMatcher(".*ERROR.*")

if (logManager.matches()) {
  error("Build failed due to ERRORs in console output")
}

Use code with caution. Learn more

This script will search the console output for the word "ERROR". If the word is found, the script will throw an error, which will cause the Jenkins build to fail.

To use this script, you will need to add it to your Jenkins pipeline. You can do this by adding the following step to your pipeline:
Groovy

stage('Check for errors') {
  steps {
    script {
      // Insert the Groovy script here
    }
  }
}

Use code with caution. Learn more

This will execute the Groovy script in the "Check for errors" stage of your pipeline. If the script finds the word "ERROR" in the console output, the build will fail.

-------------------------------

10. What are active and reactive parameters (Dynamic parameterization) in Jenkins ?

Ans :

In Jenkins, active and reactive parameters are types of dynamic parameters that allow you to build more complex parameterized jobs. Unlike static parameters, which have fixed values, dynamic parameters can be generated based on the values of other parameters or external data sources.

Active Parameters

Active parameters are generated from a Groovy or Scriptlet script. The script is executed when the parameter is displayed, and the result of the script is used to populate the parameter values. This allows you to generate parameter values based on any arbitrary logic.

For example, you could use an active parameter to generate a list of files in a directory, or to query a database for a list of available options.

Reactive Parameters

Reactive parameters are a type of active parameter that can be updated dynamically based on the values of other parameters. This means that the parameter values will change as the user selects different values for other parameters.

For example, you could use a reactive parameter to display a list of cities based on the selected state.

Dynamic Parameterization

Dynamic parameterization is a general term that refers to the use of active and reactive parameters to build more complex parameterized jobs. It allows you to create jobs that are more flexible and adaptable, and that can be used to automate a wider range of tasks.

Benefits of Active and Reactive Parameters

    Increased flexibility: Dynamic parameters allow you to build more flexible jobs that can be adapted to a wider range of tasks.

    Reduced manual effort: By generating parameter values automatically, you can reduce the amount of manual effort required to run your jobs.

    Improved data accuracy: By retrieving parameter values from external data sources, you can ensure that your jobs always have access to the most up-to-date data.

Use Cases for Active and Reactive Parameters

    Conditional execution: You can use dynamic parameters to conditionally execute sections of your job. For example, you could use a dynamic parameter to determine which tests to run.

    Data-driven testing: You can use dynamic parameters to generate data for test cases. This can be useful for testing APIs and generating realistic user input.

    Resource provisioning: You can use dynamic parameters to provision resources, such as EC2 instances or Azure VMs. This can be useful for automating the deployment of applications.

---------------------------------------


11. How to customize the build number display to something else in Jenkins job page?
Ans :


In Jenkins, you can customize the display of the build number on the Jenkins job page by using the "Build Name and Description Setter" plugin. This plugin allows you to set a custom build name and description for each build, providing flexibility in how you want to represent and identify your builds.

Here are the steps to customize the build number display:

1. **Install the Build Name and Description Setter Plugin:**
   - Navigate to "Manage Jenkins" -> "Manage Plugins" -> "Available" tab.
   - Search for "Build Name and Description Setter" in the list.
   - Select the checkbox next to the plugin and click "Install without restart."

2. **Configure the Build Name and Description Setter in Your Jenkins Job:**
   - Open the Jenkins job for which you want to customize the build number display.
   - In the job configuration, scroll down to the "Post-build Actions" section.
   - Click on "Add post-build action" and select "Set build name."

3. **Specify the Build Name:**
   - In the "Set build name" section, you can define the build name using various tokens, including environment variables, build parameters, and more.
   - For example, you can use the following as the build name: `MyCustomBuild-${BUILD_NUMBER}`.

4. **Save the Job Configuration:**
   - Save the job configuration.

Now, when you build this job, the customized build name will be displayed on the Jenkins job page instead of the default build number.

**Additional Tips:**
- You can use any combination of text and tokens to create a meaningful and customized build name. For example, incorporating information about the branch, environment, or any other relevant details.
- The same plugin allows you to set a custom build description as well, providing additional context for each build.

Here are some examples of custom build names that you can use:

-   `$JENKINS_URL/$JOB_NAME/$BUILD_NUMBER`
-   `job-$JOB_NAME-build-$BUILD_NUMBER`
-   `$BRANCH-build-$BUILD_NUMBER`

Using the "Build Name and Description Setter" plugin gives you the flexibility to represent your builds in a way that makes sense for your project or team, providing a more meaningful and customized display on the Jenkins job page.







---------------------------------

13. What are multi branch pipeline?

Ans :

In Jenkins, a Multi-Branch Pipeline is a type of pipeline that automatically discovers, manages, and builds branches in a version control repository. It's particularly useful for projects with multiple branches, such as feature branches, bug fix branches, or release branches. Multi-Branch Pipelines are often associated with Jenkinsfile-based pipelines and are designed to automate the process of creating and managing Jenkins pipelines for each branch in a version control system.

Multi-branch pipelines are a good choice for teams that develop and release software frequently. They can help to save time and effort, and they can also help to ensure that new features and bug fixes are tested and deployed quickly and reliably.

Here are key characteristics and concepts associated with Multi-Branch Pipelines:

1. **Automatic Branch Discovery:**
   - Multi-Branch Pipelines automatically discover branches in your version control system (e.g., Git, Mercurial) and create individual Jenkins pipelines for each branch.

2. **Jenkinsfile-Based Configuration:**
   - The pipeline configuration for each branch is typically defined in a `Jenkinsfile` stored within the branch. The `Jenkinsfile` contains the pipeline steps, stages, and configurations.

3. **Branch Indexing:**
   - Jenkins periodically performs branch indexing to detect new branches and remove branches that are no longer present. This ensures that the Multi-Branch Pipeline stays up-to-date with the branches in the repository.

4. **Isolation of Pipelines:**
   - Each branch has its own isolated Jenkins pipeline, allowing you to build, test, and deploy changes independently for each branch.

5. **Parallel Execution:**
   - Multi-Branch Pipelines can trigger parallel builds for multiple branches simultaneously. This can be beneficial for projects with a large number of branches that need to be tested concurrently.

6. **Integration with Code Review Systems:**
   - Multi-Branch Pipelines often integrate seamlessly with code review systems (e.g., GitHub, Bitbucket) and automatically create pipelines for pull requests. This allows you to validate changes before they are merged into the main branch.

7. **Branch-Specific Configuration:**
   - You can customize the configuration for each branch by providing a branch-specific `Jenkinsfile` or by using pipeline syntax to conditionally execute steps based on the branch.

8. **Visualization of Branch Status:**
   - Jenkins provides a user interface that visualizes the status of each branch, indicating whether the builds are passing or failing. This makes it easy to monitor the health of multiple branches.

In summary, Multi-Branch Pipelines in Jenkins provide a convenient and automated way to manage and build branches in version control systems. They streamline the CI/CD process for projects with multiple branches, ensuring that each branch is tested and validated independently. The use of Jenkinsfiles allows for a flexible and version-controlled definition of the pipeline configuration for each branch.



------------------------


14. What is shared library in Jenkins ?


In Jenkins, a shared library is a powerful and reusable way to define and manage external code in the form of scripts, functions, and variables that can be used across multiple Jenkins pipelines. Shared libraries promote code reuse, maintainability, and consistency in Jenkins pipeline development.

Key aspects of Jenkins Shared Libraries:

1. **Reusability:**
   - Shared libraries allow you to define functions, classes, and other code artifacts in external repositories that can be reused across multiple pipelines or projects.

2. **Centralized Codebase:**
   - Shared libraries are typically stored in a version-controlled repository (e.g., Git) and can be centrally managed. This promotes a single source of truth for shared code logic and facilitates versioning.

3. **Encapsulation of Logic:**
   - Shared libraries encapsulate common logic and functionality, allowing pipeline developers to focus on high-level pipeline structure and business logic without duplicating code.

4. **Standardization:**
   - By using shared libraries, organizations can enforce coding standards, best practices, and security policies consistently across all Jenkins pipelines.

5. **Maintenance and Updates:**
   - Updates or changes to shared libraries are centralized, making it easier to manage and propagate improvements or bug fixes across all pipelines that use the library.

6. **Separation of Concerns:**
   - Shared libraries enable a clear separation of concerns between pipeline orchestration and shared code. Pipeline authors can concentrate on pipeline-specific logic, while shared libraries handle common tasks.

7. **Easy Integration:**
   - Jenkins Shared Libraries seamlessly integrate with Jenkins pipelines, providing an efficient way to share and manage code without duplicating it in every Jenkinsfile.

To implement a shared library in Jenkins:

- Create a repository containing the shared library code.
- Configure Jenkins to use the shared library either at the global level or on a per-pipeline basis.
- Refer to the shared library functions and code within Jenkins pipelines.

Here are some of the ways that you can use shared libraries in Jenkins:

-   **Defining your own pipeline steps:** You can use shared libraries to define your own pipeline steps. This can be useful for encapsulating common tasks or for providing custom functionality.
    
-   **Sharing pipeline configuration:** You can share pipeline configuration between different jobs. This can be useful for setting up common environment variables or for defining global pipeline options.
    
-   **Reusing pipeline scripts:** You can reuse pipeline scripts between different jobs. This can be useful for automating common tasks or for providing custom functionality.
- 
Overall, Jenkins Shared Libraries are a valuable feature for organizations looking to improve code maintainability, enforce standards, and streamline the development of Jenkins pipelines across their projects.


-----------------
-------------------
------------------


# UNIX & SHELL SCRIPTING
-----------
14. Command to find empty files in a given directory?
ANS :

To find empty files in a given directory, you can use the `find` command along with the `-empty` option. Here's the command:

```bash
find /path/to/directory -type f -empty
```

Explanation:

- `find`: The command for searching files and directories.
- `/path/to/directory`: Replace this with the actual path to the directory you want to search.
- `-type f`: Specifies that you are looking for files (not directories or other types of files).
- `-empty`: Specifies that you want to find files that are empty.

This command will list all empty files within the specified directory and its subdirectories. If you want to limit the search to only the specified directory (excluding subdirectories), you can use the `-maxdepth` option:

```bash
find /path/to/directory -maxdepth 1 -type f -empty
```

In this command, `-maxdepth 1` restricts the search to the specified directory without descending into subdirectories. Adjust the path according to your specific use case.


---------------------------------------

16. Commands you will use it for configuring ssh connectivity between 2 machines and what files will be present in .ssh folder?

ANS :




To configure SSH connectivity between two machines, you typically need to perform the following steps. Below are the commands you might use, along with an explanation of what each command does. Additionally, I'll mention the common files you might find in the `.ssh` folder:

1. **Generate SSH Key Pair (if not already done):**
   - Run the following command on the machine from which you want to connect to the other machine:

     ```bash
     ssh-keygen -t rsa -b 2048
     ```

   This command generates an RSA key pair (public and private keys) in the default location (`~/.ssh/id_rsa`).

2. **Copy Public Key to Remote Machine:**
   - Use the following command to copy your public key to the remote machine. Replace `<remote-user>` and `<remote-host>` with the appropriate values.

     ```bash
     ssh-copy-id <remote-user>@<remote-host>
     ```

   This command appends your public key to the `authorized_keys` file on the remote machine, allowing you to authenticate without a password.

3. **Alternatively: Manually Copy Public Key to Remote Machine:**
   - If `ssh-copy-id` is not available, you can manually copy the public key using:

     ```bash
     cat ~/.ssh/id_rsa.pub | ssh <remote-user>@<remote-host> 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
     ```

   This achieves the same result as `ssh-copy-id` by appending the public key to the `authorized_keys` file on the remote machine.

4. **Secure SSH Configuration (Optional):**
   - Optionally, you may want to secure your SSH configuration by modifying the `sshd_config` file on the remote machine:

     ```bash
     sudo nano /etc/ssh/sshd_config
     ```

     Ensure the following settings:
     ```plaintext
     PasswordAuthentication no
     PermitRootLogin no
     ```

     Then, restart the SSH service:
     ```bash
     sudo service ssh restart
     ```

   These settings enhance the security of your SSH setup.

5. **Common Files in `.ssh` Folder:**
   - After these steps, you might find the following files in the `.ssh` folder:

     - `id_rsa`: Your private key (keep this secure, don't share it).
     - `id_rsa.pub`: Your public key (can be shared with others).
     - `authorized_keys`: On the remote machine, this file contains the list of public keys authorized for passwordless login.

By following these steps and commands, you should be able to set up SSH connectivity between two machines securely. Adjust the usernames, hostnames, and file paths as needed for your specific environment.





The `.ssh` folder contains the SSH configuration files and keys. The following files are typically present in the `.ssh` folder:

-   `id_rsa`: This is the private key file.
-   `id_rsa.pub`: This is the public key file.
-   `config`: This is the SSH configuration file.
-   `known_hosts`: This is a file that contains the host keys of the servers that you have connected to in the past.



---------------------------------------

17. How to schedule a shell script in unix machines?

ANS :

To schedule the execution of a shell script on Unix machines, you can use the `cron` system scheduler. The `cron` scheduler allows you to automate the execution of tasks at specified intervals. Here's a step-by-step guide on how to schedule a shell script using `cron`:

1. **Edit the Cron Table:**
   - Open the crontab file for editing using the following command:

     ```bash
     crontab -e
     ```

   If this is the first time you're editing the crontab, you may be prompted to choose an editor.

2. **Schedule the Script:**
   - In the crontab file, add a new line to specify the schedule and command to execute. The general syntax for scheduling a task is as follows:

     ```plaintext
     minute hour day month day_of_week command_to_execute
     ```

   Replace each field with the appropriate values. For example, to run a script every day at 2:30 PM, you would add:

     ```plaintext
     30 14 * * * /path/to/your/script.sh
     ```

   In this example:
   - `30` is the minute (0-59).
   - `14` is the hour (0-23).
   - `*` for day, month, and day_of_week means "every day."

3. **Save and Exit:**
   - Save the crontab file and exit the editor. The process for saving and exiting depends on the editor you chose.

     - In Vim, for example, you can press `Esc`, type `:wq`, and then press `Enter`.

4. **Verify the Cron Job:**
   - You can list your current cron jobs using the following command:

     ```bash
     crontab -l
     ```

   This will display the scheduled tasks in the crontab.

**Additional Tips:**
- **Specify the Full Path:**
  - Always use the full path to the script in the crontab to avoid issues with the working directory. For example:

    ```plaintext
    30 14 * * * /full/path/to/your/script.sh
    ```

- **Redirect Output:**
  - If your script produces any output (e.g., prints to stdout or stderr), it's a good practice to redirect the output to a file to capture any potential errors:

    ```plaintext
    30 14 * * * /full/path/to/your/script.sh >> /path/to/logfile.log 2>&1
    ```

- **Testing:**
  - Before scheduling a script, you may want to test it manually to ensure that it behaves as expected.

By following these steps, you can schedule the execution of a shell script using `cron` on Unix machines. Adjust the schedule and paths based on your specific requirements.


---------------------------------------

18. Command to get load average ?

ANS :

To get the load average on a Unix-based system, you can use the `uptime` command. The load average provides a snapshot of the system's resource usage over a specific time period. Here's how you can use the `uptime` command:

```bash
uptime
```

The `uptime` command typically outputs information about the current time, how long the system has been running, the number of users, and the load averages for the last 1, 5, and 15 minutes.

For example:

```plaintext
$ uptime
14:32:07 up  7:57,  2 users,  load average: 0.05, 0.09, 0.12
```

In this output, the load average is represented by three values separated by commas. These values correspond to the average number of processes in the run queue over the last 1, 5, and 15 minutes, respectively.

- Load Average (1 minute): 0.05
- Load Average (5 minutes): 0.09
- Load Average (15 minutes): 0.12

The load average is an essential metric for assessing system performance and can help identify periods of high demand or potential resource contention. Higher load averages generally indicate increased system activity. The specific thresholds for what constitutes a high load average may vary based on the system's configuration and the nature of the workloads it handles.


OR 

**2. `top`**

The `top` command displays a real-time view of the system's resource usage, including the CPU usage, memory usage, and process information. The load average is displayed in the first line of output.

Bash

```
$ top

```

Use code with caution. [Learn more](https://bard.google.com/faq#coding)

**3. `cat /proc/loadavg`**

The `/proc/loadavg` file contains the system's load average. You can use the `cat` command to display the contents of the file.

Bash

```
$ cat /proc/loadavg
0.01 0.05 0.08

```

Use code with caution. [Learn more](https://bard.google.com/faq#coding)



---------------------------------------

19. Need to identify ip addresses in log file and count of ip addresses in log file?

ANS :

To identify IP addresses in a log file and count the occurrences of each unique IP address, you can use a combination of command-line tools such as `grep`, `awk`, `sort`, and `uniq`. Here's an example command pipeline:

```bash
grep -oE "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b" your_log_file.log | sort | uniq -c
```

Explanation of each part of the command:

1. **`grep -oE "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b"`:**
   - `-o`: Only print the matched parts of a matching line.
   - `-E`: Interpret the pattern as an extended regular expression (ERE).
   - `\b`: Word boundary to ensure that we match complete IP addresses.
   - `([0-9]{1,3}\.){3}[0-9]{1,3}`: Regular expression to match IPv4 addresses.
     - `([0-9]{1,3}\.)`: Matches one to three digits followed by a dot, repeated three times.
     - `[0-9]{1,3}`: Matches one to three digits.
   - `\b`: Word boundary.

2. **`sort`:**
   - Sorts the list of IP addresses. This is necessary for the next step.

3. **`uniq -c`:**
   - `-c`: Prefix lines with the number of occurrences.
   - Counts the occurrences of each unique IP address.

Replace `your_log_file.log` with the actual path to your log file. This command will output a list of unique IP addresses along with their respective occurrence counts.

For example, the output might look like:

```plaintext
   3 192.168.1.1
   5 203.0.113.42
   2 10.0.0.5
   ...
```

This indicates that `192.168.1.1` appears 3 times, `203.0.113.42` appears 5 times, and so on. Adjust the regular expression if your log file contains a different format for IP addresses, and customize the command based on your specific requirements.


---------------------------------------




-----------------
-------------------
------------------


# ANSIBLE
------------
19. Why ansible ? What makes ansible powerful than other tools like chef and puppet?

ANS :




---------------------------------------

20. 5 modules that you have worked on? Can we create custom module ?

ANS :




---------------------------------------

21. What is dynamic inventory in ansible?

ANS :




---------------------------------------

22. Lets say I have both Ubuntu and centos machines as nodes I want install application tree using same playbook, how would you approach this scenario? 

ANS :




---------------------------------------

23. How to handle prompts with ansible playbook?

ANS :




---------------------------------------




-----------------
-------------------
------------------


# DOCKER
----------
24. What does ONBUILD instruction do in Dockerfile?

Ans :

The `ONBUILD` instruction in a Dockerfile is used to add triggers to the image that is being built. When you include an `ONBUILD` instruction in a parent Dockerfile, the specified commands are not executed during the build of that image. Instead, they are recorded and stored in the image metadata. These recorded commands become triggers for when the image is used as the base for another Docker image.

Here's how it works:

1. **Parent Dockerfile:**
   - In the parent Dockerfile, you include an `ONBUILD` instruction along with other instructions. For example:
     ```dockerfile
     ONBUILD COPY . /app
     ONBUILD RUN make /app
     ```

2. **Building the Parent Image:**
   - When you build the parent image using this Dockerfile, the `ONBUILD` instructions are not executed at this stage. Instead, they are recorded to be executed later.

3. **Child Dockerfile:**
   - When you use the parent image as the base for another image (the child image), the recorded `ONBUILD` instructions are triggered. For example, if the child image is as simple as:
     ```dockerfile
     FROM parent-image
     ```
   - Then, during the build of the child image, the recorded `ONBUILD` instructions (`COPY . /app` and `RUN make /app` in this case) are executed.


For example, consider a scenario where you have a base image for a Node.js application. You want to use this base image to build different production and staging environments. In the base image, you can use the `ONBUILD` instruction to define instructions for installing Node.js modules and copying the application's source code. Then, when you build the production and staging images, you can use the base image and simply provide the specific configuration values for each environment.

Here's an example of how to use the `ONBUILD` instruction:

Dockerfile

```
FROM nginx:alpine

ONBUILD RUN apk add --no-cache nodejs

ONBUILD COPY app/ /app

ONBUILD CMD ["node", "index.js"]

```

Use code with caution. [Learn more](https://bard.google.com/faq#coding)

In this example, the `ONBUILD` instruction is used to define three instructions:

1.  Install Node.js
    
2.  Copy the application's source code to the `/app` directory
    
3.  Set the entrypoint to `node index.js`
    

When you build an image from this Dockerfile, the `ONBUILD` instructions will be ignored. However, if you use this image as the base image for another image, the `ONBUILD` instructions will be executed in the context of the downstream build. For example, if you create a Dockerfile for the production environment that uses this base image, you can simply add the following lines:

Dockerfile

```
FROM my-base-image

ENV NODE_ENV=production

```

Use code with caution. [Learn more](https://bard.google.com/faq#coding)

This will create a new image that uses the `my-base-image` as the base image and sets the `NODE_ENV` environment variable to `production`. When this image is built, the `ONBUILD` instructions from the base image will be executed, ensuring that the application is configured correctly for the production environment.

The `ONBUILD` instruction can be used with any valid Docker instruction, including `RUN`, `COPY`, `CMD`, `ENV`, and so on. This makes it a versatile tool for customizing and managing base images in Dockerfiles.


The purpose of `ONBUILD` is to allow the parent image to define certain behaviors or actions that should be taken when the image is used as a base for other images. It's often used to automate common tasks or configurations that are shared across multiple child images. However, its usage has become less common over time, and alternative approaches, such as using explicit instructions in child images, are often recommended for better clarity and control over the build process.


------------

25. What is the use of .dockerignore file?

Ans :

The `.dockerignore` file is used in Docker to specify files and directories that should be excluded from the build context when building a Docker image. The build context is the set of files and directories that are sent to the Docker daemon during the build process.

Here's why the `.dockerignore` file is useful:

1. **Reduce Build Context Size:**
   - The build context is sent to the Docker daemon, and it affects the efficiency of the build process. By using a `.dockerignore` file, you can exclude unnecessary files and directories from the build context, reducing its size.

2. **Faster Builds:**
   - A smaller build context results in faster build times because there is less data to transfer to the Docker daemon. This is particularly important when dealing with large projects or when working in environments with limited network bandwidth.

3. **Avoiding Unwanted Files in the Image:**
   - The `.dockerignore` file helps ensure that certain files or directories are not inadvertently included in the final Docker image. This is important for keeping the image size as small as possible and excluding files that are not needed for the application to run.

4. **Avoiding Sensitive Information:**
   - It is a good practice to use the `.dockerignore` file to exclude sensitive information, such as credentials or secret keys, from being unintentionally included in the Docker image.

5. **Clearer and More Predictable Builds:**
   - By explicitly specifying files and directories to ignore, the `.dockerignore` file makes the build process more predictable and helps avoid unexpected inclusions in the image.

Here's a simple example of a `.dockerignore` file:

```plaintext
# Ignore files and directories
node_modules
*.log
secret.txt
logs/
test/

```

In this example, the `node_modules` directory, log files, and a file named `secret.txt` would be excluded from the build context.


When you build a Docker image, the Docker daemon will read the `.dockerignore` file and ignore any files or directories that are listed in the file. This means that these files and directories will not be included in the image.


In summary, the `.dockerignore` file is a valuable tool for optimizing Docker builds, improving build performance, and ensuring that only necessary and desired files are included in the Docker image.


------------

26. I have dockerfile that accepts arguments, if I supply value as “1” then it should use maven 2.x version for base image and if I supply “2” then it should take maven latest as base image 

Ans :

To achieve conditional behavior in a Dockerfile based on the provided build arguments, you can use the `ARG` instruction to define build-time variables, and then use conditional statements based on those variables. Here's an example of how you can conditionally choose the base image version depending on the value of a build argument:

```Dockerfile
# Define a build argument with a default value
ARG MAVEN_VERSION=1

# Use a multi-stage build with a builder stage
FROM maven:${MAVEN_VERSION} as builder

# Copy your application source code
COPY . /app

# Run Maven build commands
RUN mvn clean install

# Final image
FROM openjdk:8-jre-alpine

# Copy artifacts from the builder stage
COPY --from=builder /app/target/your-application.jar /app/

# Set the command to run your application
CMD ["java", "-jar", "/app/your-application.jar"]
```

In this example:

1. The `ARG` instruction defines a build argument named `MAVEN_VERSION` with a default value of `1`.

2. The first `FROM` instruction uses the `MAVEN_VERSION` build argument to choose the Maven base image version. If the build argument is not provided during the build, it defaults to version 1.

3. The subsequent instructions perform the necessary build steps using the specified Maven version.

4. The second `FROM` instruction starts a new stage of the build for the final image. It uses a lightweight base image (in this case, `openjdk:8-jre-alpine`), and it copies artifacts from the builder stage.

5. The `CMD` instruction sets the default command to run your application.

To build the Docker image, you can use the following commands:

```bash
# Build with Maven 2.x
docker build --build-arg MAVEN_VERSION=2 -t your-image-name .

# Build with Maven latest
docker build --build-arg MAVEN_VERSION=latest -t your-image-name .
```

To build the Docker image using the latest Maven version, you would run the following command:

```
docker build -t my-app:latest --build-arg MAVEN_VERSION=3.8.4 .

```

By specifying the `--build-arg` flag during the build, you can dynamically choose the Maven version based on the supplied argument.


-----------

27. What are docker compose and docker swarm?

Ans :



**Docker Compose:**
Docker Compose is a powerful tool designed for defining and managing multi-container Docker applications. Using a declarative YAML file, typically named `docker-compose.yml`, you can specify the entire application stack, including services, networks, and volumes. This approach simplifies the deployment and management of complex applications, especially those following microservices architectures.

Key Features of Docker Compose:

1. **Declarative Configuration:**
   - Docker Compose uses a YAML file to define the configuration of your application, making it easy to understand and version the entire application stack.

2. **Multiple Container Orchestration:**
   - Docker Compose allows you to define and orchestrate multiple containers that work together as a single application, facilitating the management of interconnected services.

3. **Environment Variables and Overrides:**
   - Customization is supported through the use of environment variables and configuration overrides, making it convenient to adapt the application behavior across different environments.

4. **Networking and Volumes:**
   - Docker Compose provides features for defining custom networks and volumes, enabling seamless communication between containers and persistent data storage.

5. **Single Command Operations:**
   - Operations like starting and stopping the entire application stack are simplified with straightforward commands like `docker-compose up` and `docker-compose down`.

**Docker Swarm:**
Docker Swarm, on the other hand, serves as a native clustering and orchestration solution for Docker. It allows you to create and manage a swarm of Docker nodes, transforming them into a single virtual Docker host. Swarm mode offers native support for orchestrating containers at scale, distributing workloads across a cluster of machines, and ensuring high availability.

Key Features of Docker Swarm:

1. **Orchestration at Scale:**
   - Docker Swarm excels in orchestrating containers at scale, providing mechanisms for deploying, scaling, and managing multi-container applications across a cluster of machines.

2. **Built-in Load Balancing:**
   - Swarm includes built-in load balancing to efficiently distribute incoming requests across multiple containers, optimizing resource utilization and ensuring high availability.

3. **Node Management:**
   - Managing a cluster of nodes, which can be physical or virtual machines, is a strength of Docker Swarm. Nodes can dynamically join or leave the swarm, providing flexibility and scalability.

4. **Service Discovery:**
   - Swarm mode includes service discovery, allowing containers to discover and communicate with each other using service names, simplifying networking in a clustered environment.

5. **Secure by Default:**
   - Security is prioritized in Swarm mode, with features such as mutual TLS authentication between nodes, ensuring a secure communication layer within the cluster.

**Choosing Between Docker Compose and Docker Swarm:**
Choosing the right tool depends on your specific needs. Docker Compose is well-suited for developing, testing, and deploying multi-container applications in a single-node environment. It simplifies local development and is an excellent choice for less complex scenarios.

On the other hand, Docker Swarm is designed for production-grade container orchestration, offering advanced features such as service discovery, load balancing, and rolling updates. It excels in managing distributed applications across multiple nodes, providing scalability and fault tolerance.

In summary, Docker Compose is ideal for local development and testing, while Docker Swarm is a robust choice for deploying and managing containerized applications in a production environment with scalability and high availability requirements.



----------------------------------
-------------------------------------


# KUBERNETES
---------
28. Components in kubernetes architecture?
Ans :

```
Master node :
 - Api server :
	 -  exposes k8 api , used by both user and components
	 -  serves as frontend of k8 control
	 - provides a RESTful API that allows users to perform CRUD Kubernetes object

 - Controller Manager :
	 - Manages controllers that regulate state of clusters
	 - Examples include the Node Controller, Replication Controller, and Endpoints Controller.

 - Cloud-controller-manager : provide integration with coud provider

 - Scheduler :
	 - assigns a node to newly created pods based on resource availability / policy/ constrains / node affinity, and anti-affinity when making scheduling decisions.

 - Etcd : 
	 - key value store that store configuration data of cluster
	 - holds state of entire cluster,  imp for maintaining cluster integrity
	 - It is used by the other control plane components to keep track of the state of the cluster.

Node/ worker :
 - kubelet : 
	  - agent that runs on each node.
	  - enure containers runningin a pod.
	  - communicat with api and manages container lifecycle.
  - kube proxy :
	   - Maintains network rules on nodes, enabling communication between pods across the cluster.
	   - It directs traffic to the appropriate pods based on their network policies.
  - Container runtime :
		  - software that runs containers
		  - responsible for creating, starting, stopping, and managing containers

Pods : smallest and simplest unit in k8 ,it represent running process in cluster and can contain one or more containers.

Service : 

Volume : directory accessible by all containers in a pod , it is used for persisting data and sharing data between containers.

Namespace : way to divide cluster resources between mutiple use/teams , resource with same name can exist in diff namespace.

Label : key value pair attached to object such as pods , label used to recognize and select objects. 
----







```


In Kubernetes architecture, there are several key components that work together to manage containerized applications. Here's a high-level overview of the main components:

1. **Master Node:**
   - **API Server:** Serves as the front end for the Kubernetes control plane. It exposes the Kubernetes API, which is used by both users and other components.
   - **Controller Manager:** Manages controllers that regulate the state of the cluster. Examples include the Node Controller, Replication Controller, and Endpoints Controller.
   - **Scheduler:** Assigns a node to newly created pods based on resource availability, policies, and constraints.

2. **Node (Minion)**
   - **Kubelet:** Ensures that containers are running in a Pod. It communicates with the API server and manages the container lifecycle.
   - **Kube Proxy:** Maintains network rules on nodes, enabling communication between pods across the cluster.
   - **Container Runtime:** The software responsible for running containers, such as Docker or containerd.

3. **etcd:**
   - A distributed key-value store that stores the configuration data of the cluster. It holds the state of the entire cluster and is crucial for maintaining cluster integrity.

4. **Pod:**
   - The smallest and simplest unit in the Kubernetes object model. A Pod represents a running process in a cluster and can encapsulate one or more containers.

5. **Service:**
   - An abstraction that defines a logical set of Pods and a policy by which to access them. It provides a stable endpoint for communication between Pods.

6. **Volume:**
   - A directory that is accessible to all containers in a Pod. Volumes are used for persisting data and sharing data between containers.

7. **Namespace:**
   - A way to divide cluster resources between multiple users or teams. It provides a scope for names. Resources with the same name can exist in different namespaces.

8. **Label:**
   - A key-value pair that is attached to objects, such as pods. Labels are used to organize and select subsets of objects.

Understanding the roles and responsibilities of these components is crucial for effective management and orchestration of containerized applications in a Kubernetes cluster.

----------------------------

30. What are stateful sets in kuberentes?

Stateful sets :
  -  provides a way to deploy and scale stateful applications that require stable network and persistent storage .
  - statefulSet is a controller used to manage the deployment and scaling of a set of Pods, while providing guarantees about the ordering and uniqueness of those Pods.

characteristics : 
* Sticky identities :  Each Pod in a StatefulSet has a unique, stable identity that persists across restarts and reschedules. This identity is based on an ordinal index,
  
* Ordered Deployment and Termination : Pods are created and terminated in a predictable order. This is crucial for applications that rely on specific startup or shutdown sequences.

* Stable storage : can optionally provide persistent storage for Pods using persistent volumes (PVs). This allows applications to store data that persists even if the Pod is restarted or rescheduled.

* Stable network :   ensure that Pods have a stable network identity, meaning their IP addresses /  hostname based on its ordinal index. For example, if you have a StatefulSet named "web," the pods could be named "web-0," "web-1," and so on. This naming convention remains consistent even if pods are rescheduled or if the StatefulSet is scaled up or down.  remain constant even if the Pod is rescheduled to a different node. This is important for applications that rely on fixed network addresses.

* Headless Service :  StatefulSets are associated with a Headless Service. A Headless Service is a service without a cluster IP, and it allows DNS resolution to the individual pods in the StatefulSet using their stable hostnames. This enables other applications to discover and connect to the pods directly.

*  Update strategy :  -   StatefulSets provide update strategies that allow you to control how updates to the StatefulSet are performed. This is important for minimizing disruption to stateful applications. The two common update strategies are RollingUpdate and OnDelete.

Use cases : Databases . message queues / Distributed systems

----------------------------

31. Command to find which container has failed in pod and command to get logs of container 

Ans :

Certainly! In Kubernetes, you can use the `kubectl` command-line tool to find which container has failed in a pod and to retrieve the logs of a specific container within that pod.

### Command to Find Failed Container in a Pod:

```bash
kubectl describe pod <pod-name>
```

```
kubectl get pods -o jsonpath='{.items[*].status.containerStatuses[*].state.terminated.reason}'


```

Replace `<pod-name>` with the actual name of your pod. Look for the "Events" section in the output. Events often provide information about the state changes in the pod. You can identify any error messages or failure events related to containers in this section.

### Command to Get Logs of a Container in a Pod:

```bash
kubectl logs <pod-name> -c <container-name>
```

- Replace `<pod-name>` with the actual name of your pod.
- Replace `<container-name>` with the name of the container for which you want to retrieve logs.

If your pod has only one container, you can omit the `-c <container-name>` part.

These commands assume you have the `kubectl` tool configured to connect to your Kubernetes cluster, and you have the necessary permissions to access the pod information and logs. The commands will provide you with insights into the status of the containers and help you troubleshoot any issues.

----------------------------

32. Tools to maintain kubernetes log files ?


Ans : 

Maintaining Kubernetes log files involves collecting, storing, and analyzing logs from various components within the Kubernetes cluster. There are several tools available to help with log management in a Kubernetes environment. Here are some commonly used tools:

1. **Elasticsearch, Logstash, and Kibana (ELK Stack):**
   - **Elasticsearch:** A distributed search and analytics engine that can store and index logs.
   - **Logstash:** A server-side data processing pipeline that ingests data from multiple sources, transforms it, and then sends it to a "stash" like Elasticsearch.
   - **Kibana:** A data visualization dashboard for Elasticsearch. It allows you to explore, visualize, and analyze the log data.

2. **Fluentd:**
   -  Fluentd is another popular open-source log aggregator that collects logs from various sources, including Kubernetes pods, and forwards them to a central location for storage and analysis. It offers flexibility in log parsing and processing, supporting a variety of output formats.

3. **Prometheus:**
   - Prometheus is a monitoring and alerting toolkit. While it's primarily used for metrics, it can also be configured to scrape and store logs. Grafana is often used in conjunction with Prometheus for log visualization.

4. **Grafana:**
   - Grafana is a popular open-source platform for monitoring and observability. It can integrate with various data sources, including Elasticsearch and Prometheus, to visualize logs and metrics.

5. **Splunk:**
   - Splunk is a powerful log management and analysis tool. It can collect, index, and correlate log data in real-time, providing powerful search and visualization capabilities.

6. **LogDNA:**
   - LogDNA is a cloud-based log management and analysis platform that is easy to set up and provides real-time log streaming, searching, and alerting.

7. **Stackdriver Logging (now part of Google Cloud Operations Suite):**
   - If you are running Kubernetes on Google Cloud, Stackdriver Logging can be integrated for collecting and analyzing logs.

8. **Loki:**
   - Loki is a horizontally scalable, highly available log aggregation system inspired by Prometheus. It is designed to be cost-effective and easy to operate.
   -  Loki is a Prometheus-based log management system that collects logs in structured text format. It stores logs in an object storage system and provides a query language for filtering and analyzing logs. Loki is relatively new but gaining popularity due to its integration with the Prometheus monitoring ecosystem.

When choosing a log management tool for Kubernetes, consider factors such as scalability, ease of integration, storage options, and the specific features required for your environment. It's also common to use a combination of tools for different aspects of log management, such as collecting, storing, searching, and visualizing logs.


----------------------
--------------------
-------------------------
AWS
-----
32. Services used AWS and tasks performed in AWS
