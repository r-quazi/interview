## Devops Interview questions | Devops Telephonic interview - 2 ( Mock Interview ) 
* mock : https://www.youtube.com/watch?v=lXGAJElFxaA&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=2
* Answers : https://www.youtube.com/watch?v=7WJ31VFk1_Y&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=10
  
------------------------------------

Q1 : Can you tell me what are tools you have used and your daily activities ?
-ans :

-----------
----
----

# Git :

Q2 : What work have you did in git like only related to devops or other as well ?
-ans :

```
Worked on :
      -  pull
      -  push, 
      -  clone ,
      -  fetch

Admin,poc,dev : 
        - access control,
        - repo management,
        - branching strategies,
        -  code reviews , 
        - issue tracking,
        - backup and recovery
        - git maintenance
        - compliance n security  , git hooks

Worked on GitWebhook for jenkins :
  - commit jenkins job trigger
  - pat token , permission 
  - github webhook : 
                  -  api ,  json paylod  , endpoint
                  -  protocols tcp udp grpc http
                  - 2 way handshake , data sent and received
                  -  new code job trigger 

Github to codecommit migrate :
  - create codecommit repo
  - clone that repo need iam role / user
  - clone  git repo
  - update origin url via command or from file in .git
  - push the repo 
  - multiple branches use --all or a script 

Github to azure repo :
  - git owned by microsoft so  backedn tech same
  - create repo
  - use import option and provide url , pat
  - done

Github to oracle : same as aws


```

And for my personal git profile i have created orgnization , i have also worked with github api to delete the repository which are more than 2 years old and do not have any activity .
here is the script :

```
#!/bin/bash

# GitHub Personal Access Token
GITHUB_TOKEN="YOUR_PAT_TOKEN"

# GitHub username or organization
USERNAME_OR_ORG="YOUR_USERNAME_OR_ORG"

# Number of days of inactivity to consider a repository as "old"
DAYS_THRESHOLD=365 # 1 year

# Function to delete a repository
delete_repository() {
    repo_name="$1"
    curl -X DELETE -H "Authorization: token $GITHUB_TOKEN" "https://api.github.com/repos/$USERNAME_OR_ORG/$repo_name"
}

# Get a list of repositories for the user or organization
repos=$(curl -s -H "Authorization: token $GITHUB_TOKEN" "https://api.github.com/users/$USERNAME_OR_ORG/repos")

# Iterate over each repository and check if it's old
for repo in $repos; do
    repo_name=$(echo "$repo" | grep -o '"name": "[^"]*' | cut -d '"' -f 4)
    last_updated=$(echo "$repo" | grep -o '"updated_at": "[^"]*' | cut -d '"' -f 4)
    last_updated_timestamp=$(date -d "$last_updated" +%s)
    current_timestamp=$(date +%s)
    inactive_days=$(( (current_timestamp - last_updated_timestamp) / 86400 )) # Calculate days since last update

    if [ $inactive_days -gt $DAYS_THRESHOLD ]; then
        echo "Deleting old repository: $repo_name"
        delete_repository "$repo_name"
    fi
done



```


----
----




Q3 : Lets say your organization has github and bitbucket to store code, you have cloned a repo onto your local and changed directory name. after some days one of your team members asks you to share clone link, how would you provide the same? The problem is you have changed cloned directory name ( by default code will cloned to directory with repo name ) , now if you search with changed directory name in github or bitbucket it wont list 

-ans :

```
-  can use the hitory command to find if we made any changes and we can pipe the command with grep to 

-  history | grep "git clone *"
-  git remote  -v
-  from configfile located in .git
-  from ducumentation
-  git creds manager
-  system logs
-  git activity notification
-  browser history

```

Whenever we clone the repository the code will be cloned in folder which has the same name as git repo , or if we downloaded zip file ithas the same name as repo , and if we changed the name of folder for example frontend-login-activity   to frontend-login-feature  and suppose if we try to find the repository using frontend-login-feature we  will be unable to find the repo on github , in this case we have several options to find the repo.

1. we can use the hitory command to find if we made any changes and we can pipe the command with grep to filter only relevant result for the name change of the folder ,
2.  Or we can do `history | grep "git clone` to find the clone URLs


3. we can use `git remote -v `  to get the URL directly .
4. We can use config file that is located in .git  folder  there will be remote repo url as well.
5. If we are mainaining documenetation or the daily tasks like in confluence or in quip we can find the changs if we have made any from the docs as well however the docs shoud have an optimized searach feature available to scan the whole document and give relevant results.
6.  We can also use git credential manager to find the details , i was working with a windows machine and i was getting some error while cloning rivate repo so i worked with git creds manager there.
7.  We can also use the system logs ( Linux ) to review the clone  commands we may have used
8.  If we have  enabled notifications for git activity we may use that as well to find the repo
9.  or the last option we hav is to check the browser history.















----
----


Q5 :  I have shell script to delete particular dependency ( repo is maven project ). before running the script i need to clone repo to my local, here point to note i should only clone master branch and only last commit ( last commit has all the code ) how would you do this?
-ans :

```

-  shallow clone
-  Clone the repository (only the 'master' branch with the latest commit) : 
`git clone --single-branch --branch master --depth 1 "$REPO_URL" "$CLONE_DIR"`

-  --depth is like tree
-  later can update via `git fetch origin master`

-   we can create archive but that will remove all git metadata

- Pros :
  -  cicd , small metadata , faster job process 
  -  reducing bandwith ... cloud
  -  helpful for automateed  code reviews, automated tasks

```

We can do this using the shllow clone. 
We can clone a single branch using the flag `--single0branch` however it will clone only master or main branch if we need to specify a particulra branch we can using `--branch <branch name>` to clone the particukar branch the we need to use `--depth  1` to clone only last commit.

So the command willl look like this :
```
# Clone the repository (only the 'master' branch with the latest commit)
git clone --single-branch --branch master --depth 1 "$REPO_URL" "$CLONE_DIR"

``` 

The `--depth ` option is like a tree where the smaller number we provide will give less details lest suppose as leaves of tree , the larger the number it ill go down more providing more details like trunk to root of tree.

After performing shallow clone with limited depeth if there is any update in the repository we can use   `git fetch origin master`  and `git reset --hard origin/master`   here we can update it to the latest commit .

now we have acheived both minimal hostory and latest code

SECOND option we have is using archive :

We can create  an archive of  particulra branch lets say master and then extract it to another location or directory , howvevr this approach may remove all the git metadata and we will have code only.

```
git archive --format=tar.gz --output=latest.tar.gz master
tar -xvf latest.tar.gz

```
This approach provides a clean snapshot of the code without any Git-related metadata.


Cloning the repo with latest commit will have recent updated code this migt be helpful in scenarios such as :
1. CICD : Since we have only last commit means we have small metadata so the jenkins server will process the job a little faster and the memory consumption will be less aswell , as we are storing/ clonihg  only required data.

2.   Reducing bandwith : If we are using EC2 for develeopers , indeed we have incoming traffic free however the utgoing traffic will have charges depending on the bandwith  , ampiunt of data transfer so fetchng onu required data will help us to mantain te cost as well , ets suppose we are creating a jenkins job then a container or storing / archiving th artifact or pushing to git repo all these are outgoing traffic .  and here we can save a cost , This can be helpful when we have 1000s of devs , testers etc.

3.  cloning single repo with less depth can also be helpful for automateed  code reviews, automated tasks ,    and we can easily manage large repositories.




----
----

 

Q6 : what is submodule and why we need submodule?
-ans :

```

-   include one git repo as a subdirectory within another git repository.
-  nested repo, submodule nested inside superproject
-  easy to manage and version control external libraries / dependencies within project

-  useful for large project dependant on other project , different teams , project relies on same set of libraries
-   isolation , version control , update and bug fix to external repo

- comands `git submodule -----`
```

Git Submodule is a mechanism whih allows us to include one git repo as a subdirectory within another git repository.

so we are nesting the repositories here, One git repo i.e submodule is nested  inside nother git repo i.e Superproject.


it is easy way to manage an version control external dependencies or libraries withih the project.


Submodules are useful when we have dependency on another project for example   You're working on a large software project that consists of multiple components, each developed and maintained by different teams. The project relies on a common set of shared libraries and utilities that are used across various components. To ensure consistency and version control, you decide to use Git submodules.



Using submodules we can  maintain seperate repositories for the services / libraries or the dependencies. instead o manually copiying and  managing these dependencies we can use submodules to  include  them as a part of project.


Other benefits of submodules include isolation -- we have a seperate code base and bad commit wont affect the whole project we have , Version control -- each module can be version contolled and we can keep track on changes as well as audits since organizations uses LDAP or IAM , active directory , maintanability -- when external dependencies receive an update or bug fixes we can easily update the submodule to latest version. 



There are few submodule commands in git :



1. **git submodule init:** Initializes submodules.

2. **git submodule update:** Updates submodules.

3. **git submodule add <repository_url> <path>:** Adds a new submodule.

4. **git submodule status:** Shows the status of submodules (e.g., whether they are up to date or have uncommitted changes).

5. **git submodule foreach \<command>:** Executes a Git command in each submodule directory.

6. **git submodule sync:** Synchronizes the submodule URL configuration in the `.gitmodules` file.

7. **git submodule deinit \<path>:** Deinitializes a submodule.

8. **git submodule absorbgitdirs:** Moves the contents of a submodule into its parent repository.










----
----

 

Q7 : Lets say you have changed 5 files a,b,c,d and e in a repo and you did git add ., now all the files are in staging area, now i decided not to commit file d. how would delete it from staging area?
-ans :


```
- git reset head d
-   git restore --staged d
-  index file : not recommended it is binary
```
If we made  changes to multiple files and these files are tracked then   we used `git add . ` to move all the files to staging area but if we want to remove some files from staging area we can use git reset feature.

So the command looks like : `git reset HEAD d`
      git reset: This command allows you to reset changes in various ways. When used with HEAD, it's typically used to unstage changes.
    HEAD: Refers to the latest commit in your branch.
    d: Represents the name of the file you want to unstage

    

After running this command, file d will be removed from the staging area, and it will remain as an unstaged change in your working directory. You can then commit the remaining changes (files a, b, c, and e) separately without including file d.


However it is not a best practice to commit multiple files with same commit id . we should small changes and each commit should be relted to a single file only so we can tracj changes easily.

another option we have is to use restore whch was inroduced in git 2.23 
To unstage file d, you can run: ` git restore --staged d`   the file will be moved from staged ( index , cache ) to unstage and we can commit the remaining files.


whenever we we move files to staging area or we are indexing the file it will be stored in cache or in index file located in .git folder,  we cant directly make changes in index file as it is not human readable it is binary file. 


To get a sense of the binary content within the .git/index file, you can use Git's plumbing command git ls-files with the --debug option, which provides a hexadecimal dump of some of the index file's content. Here's how you can use it:
To interact with the index or staging area, it's recommended to use Git's high-level commands, such as git add, git reset, and git status, which provide a more user-friendly interface for managing and querying the staging area's state.



----
----

# Maven :


Q8 :  what is multi module project in maven and what are the setting you want to do in multi module parent and child project ? what is dependency management ?
-ans :

**Multi-module projects in Maven:**

A multi-module project in Maven is a project that consists of multiple subprojects or modules. These modules are typically related and together form a larger project. Maven provides a way to structure and manage such projects by using a parent POM (Project Object Model) and individual POMs for each module.

**Key Components:**

1. **Parent POM:**
   - The parent POM is at the root of the project hierarchy and contains common configurations, settings, and dependencies shared across all modules.
   - It can define plugins, properties, and repositories that are applicable to all modules.
   - The `<modules>` element in the parent POM lists all the child modules.

2. **Child Modules:**
   - Each module corresponds to a subproject within the multi-module project.
   - Each module has its own POM file specifying its unique configuration, dependencies, and build settings.
   - Modules can have dependencies on each other.

**Settings in Multi-Module Parent Project:**

1. **POM Configuration:**
   - Define common configurations, properties, and plugin configurations shared by all modules.
   - Use the `<modules>` element to list all child modules.

2. **Dependency Management:**
   - Define dependency versions in the `<dependencyManagement>` section.
   - Child modules can then inherit these versions without explicitly specifying them.

3. **Build Configuration:**
   - Configure build plugins that are common across modules.
   - Specify profiles if needed for different build configurations.

4. **Reporting:**
   - Configure reporting plugins for generating reports across all modules.

**Settings in Child Modules:**

1. **POM Configuration:**
   - Specify module-specific configurations, properties, and plugin configurations.
   - Define dependencies unique to the module.

2. **Inheritance:**
   - Inherit configurations from the parent POM.
   - Override or extend configurations as needed.

3. **Build Configuration:**
   - Configure build plugins specific to the module.
   - Specify goals and phases relevant to the module.

4. **Dependencies:**
   - Declare dependencies specific to the module.
   - Utilize the `<dependencyManagement>` section from the parent POM for version management.

**Dependency Management:**

In Maven, dependency management involves centralizing and versioning dependency information. This is achieved through the `<dependencyManagement>` section, typically defined in the parent POM. It allows you to specify the version of a dependency in one place, and all child modules can inherit that version without explicitly specifying it.

**Example:**

Parent POM (`pom.xml`):
```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>multi-module-parent</artifactId>
    <version>1.0.0-SNAPSHOT</version>

    <packaging>pom</packaging>

    <modules>
        <module>module-a</module>
        <module>module-b</module>
    </modules>

    <dependencies>
        <!-- Dependency versions managed in parent -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.3.10</version>
        </dependency>
    </dependencies>
</project>
```

Child Module (`module-a/pom.xml`):
```xml
<project>
    <parent>
        <groupId>com.example</groupId>
        <artifactId>multi-module-parent</artifactId>
        <version>1.0.0-SNAPSHOT</version>
    </parent>

    <modelVersion>4.0.0</modelVersion>
    <artifactId>module-a</artifactId>
    <dependencies>
        <!-- No need to specify version for spring-core -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
        </dependency>
    </dependencies>
</project>
```

This example demonstrates how the parent POM manages the version of the `spring-core` dependency, and child modules inherit this version without specifying it explicitly.

-----------------------

Q9 : what is transitive dependency ?
-ans :
A transitive dependency in software development refers to a situation where a project depends not only on a direct dependency but also on all the dependencies of that direct dependency. In other words, it is a chain of dependencies that are brought into a project due to the inclusion of a direct dependency.

Here's a breakdown of the concept:

1. **Direct Dependency:**
   - A direct dependency is a library or module explicitly specified in your project's dependencies.

2. **Transitive Dependency:**
   - When you add a direct dependency to your project, it may itself depend on other libraries (its own dependencies).
   - These indirect dependencies, which are not explicitly specified in your project but are brought in by your direct dependency, are called transitive dependencies.

**Example:**

Let's consider a simplified example:

```plaintext
Project A (Direct Dependency)
|-- Dependency X (Transitive Dependency)
   |-- Dependency Y (Transitive Dependency)
   |-- Dependency Z (Transitive Dependency)
```

In this example:

- You have Project A, which depends directly on Dependency X.
- Dependency X, in turn, depends on Dependency Y and Dependency Z.
- Dependency Y and Dependency Z are transitive dependencies for Project A.

**Key Points:**

- Transitive dependencies can introduce a chain of dependencies, and it's crucial to manage them properly to avoid version conflicts or unexpected behavior.
- Build tools like Maven, Gradle, and npm automatically resolve and manage transitive dependencies, ensuring that the correct versions are used.
- Understanding and managing transitive dependencies is essential for maintaining a clean and efficient project structure.
- Dependency management tools often provide mechanisms to exclude or override transitive dependencies when needed.

In summary, a transitive dependency is an indirect dependency that enters your project through a direct dependency, forming a chain of dependencies. Properly managing these dependencies is a critical aspect of building and maintaining software projects.


-------------------------------------------


----------------
----------------
-----------------


# JENKINS : 

Q10 : Have you worked on commit based job in jenkins? what settings you need to do in jenkins and github to setup commit based job?

-ans :
Yes, I have experience setting up commit-based jobs in Jenkins. Here's an outline of the steps and configurations needed in Jenkins and GitHub to establish a commit-based job:

**Setting Up a Commit-Based Job in Jenkins:**

1. **Install Jenkins GitHub plugin:**
   - Ensure that the GitHub plugin is installed in Jenkins. You can install it through the Jenkins Plugin Manager.

2. **Configure GitHub credentials:**
   - In Jenkins, go to "Manage Jenkins" > "Manage Credentials."
   - Add GitHub credentials (username and password or personal access token) that Jenkins will use to interact with the GitHub repository.

3. **Create a new Jenkins job:**
   - Create a new freestyle or pipeline job in Jenkins.

4. **Configure Source Code Management (SCM):**
   - In the job configuration, go to the "Source Code Management" section.
   - Select "Git" as the SCM.
   - Provide the GitHub repository URL.
   - Choose the GitHub credentials configured earlier.

5. **Set up Build Triggers:**
   - In the job configuration, go to the "Build Triggers" section.
   - Select the option for "GitHub hook trigger for GITScm polling" or "Poll SCM" if you want Jenkins to check for changes at regular intervals.

6. **Define Build Steps:**
   - Configure the build steps based on your project requirements.
   - For example, you can include build, test, and deployment steps.

7. **Save and Build:**
   - Save the Jenkins job configuration.

**Setting Up GitHub for Jenkins Integration:**

1. **Configure Webhook in GitHub:**
   - Go to your GitHub repository.
   - Navigate to "Settings" > "Webhooks" > "Add webhook."
   - In the Payload URL, provide the Jenkins webhook URL. This is typically in the format: `http://jenkins-server/github-webhook/`

2. **Set Up Secret (Optional):**
   - You can configure a secret token for enhanced security.
   - In the webhook configuration, set a secret token, and configure the same token in Jenkins.

3. **Test Webhook:**
   - After configuring the webhook, you can test it to ensure that GitHub can trigger Jenkins builds.

4. **Configure Jenkins Build Status (Optional):**
   - To display build status in GitHub pull requests, you can enable the "GitHub Pull Request Builder" plugin in Jenkins.
   - Configure the plugin to update the build status in GitHub.

By completing these steps, you've set up a Jenkins job that is triggered on every commit to the associated GitHub repository. The integration allows Jenkins to automatically build and test the code whenever changes are pushed to the repository.

-------------------------

Q11 :  you want to create 50 freestyle jobs with same configurations, but only change is job name. how would you achieve teh same?
-ans :

To create 50 freestyle jobs with the same configurations but different job names, you can use the Jenkins Job DSL plugin. This plugin allows you to define jobs programmatically using a Groovy-based DSL (Domain-Specific Language).

Here are the steps to achieve this:

1. **Install Jenkins Job DSL Plugin:**
   - In the Jenkins dashboard, go to "Manage Jenkins" > "Manage Plugins."
   - Install the "Job DSL" plugin from the available plugins.

2. **Create a Seed Job:**
   - Create a new freestyle job in Jenkins, known as the "Seed Job."
   - Configure this job to execute the Jenkins DSL scripts.

3. **Configure the Seed Job:**
   - Add a build step in the Seed Job to execute a DSL script.
   - Write a DSL script that defines the common configuration for the 50 jobs and creates them with unique names.

   Example DSL script (`createJobs.groovy`):
   ```groovy
   for (int i = 1; i <= 50; i++) {
       job("JobName_${i}") {
           // Define common job configurations here
           // ...
       }
   }
   ```

4. **Run the Seed Job:**
   - Build the Seed Job to execute the DSL script.
   - This will dynamically create 50 freestyle jobs with unique names.

5. **Adjust DSL Script for Configuration Changes:**
   - If there are changes to the common configuration, modify the DSL script accordingly and re-run the Seed Job.
   - This ensures that all 50 jobs are updated with the new configuration.

By using the Jenkins Job DSL plugin, you can automate the creation and maintenance of multiple jobs with similar configurations. It provides a flexible and efficient way to manage a large number of jobs programmatically.

Additionally, you can version control the DSL script, making it easier to track changes and roll back configurations if needed. This approach is particularly useful when dealing with a large number of jobs that share common settings.

---------------------------------
--------------------------
-----------------------


# LINUX :



Q12 :  write a script which accepts file or folder, if its folder delete it else print "this is a file"?
-ans :

Certainly! Here's a simple shell script that accepts a file or folder as an argument. If it's a folder, it deletes it, and if it's a file, it prints "this is a file":

```bash
#!/bin/bash

# Check if an argument is provided
if [ $# -eq 0 ]; then
    echo "Please provide a file or folder as an argument."
    exit 1
fi

# Check if the provided path exists
if [ -e "$1" ]; then
    # Check if it's a directory
    if [ -d "$1" ]; then
        # If it's a directory, delete it
        echo "Deleting the folder: $1"
        rm -r "$1"
    else
        # If it's a file, print a message
        echo "This is a file: $1"
    fi
else
    echo "The provided path does not exist: $1"
fi
```

Save this script in a file (e.g., `check_file_or_folder.sh`), make it executable (`chmod +x check_file_or_folder.sh`), and then you can use it like this:

```bash
./check_file_or_folder.sh /path/to/your/file_or_folder
```

Replace `/path/to/your/file_or_folder` with the actual file or folder path you want to check. The script will then either delete the folder or print "this is a file" based on the provided input.

----------------------------------


Q13 : How to check whether particular port is already in use or not ?
-ans :

```
- sudo nmap -p-localhost
- sudo lsof -i -P -n | grep LISTEN
- ss -tulpn
- netstat -tulpn | grep <port_number>

```

To check whether a particular port is already in use, you can use various command-line tools depending on your operating system. Here are examples for Linux, macOS, and Windows:

**Linux / macOS:**

You can use the `netstat` or `lsof` command to check for port usage.

Using `netstat`:
```bash
netstat -tulpn | grep <port_number>
```

Using `lsof`:
```bash
lsof -i :<port_number>
```

Replace `<port_number>` with the actual port number you want to check.

**Windows:**

On Windows, you can use the `netstat` command as well.

```cmd
netstat -ano | find "LISTENING" | find "<port_number>"
```

Replace `<port_number>` with the actual port number you want to check.

Alternatively, you can use the `Test-NetConnection` cmdlet in PowerShell:

```powershell
Test-NetConnection -ComputerName localhost -Port <port_number>
```

Replace `<port_number>` with the actual port number you want to check.

**Example Output:**

If the port is in use, the output will show the process ID (PID) or the name of the process using that port. If the port is not in use, there will be no output.

Remember that if you are checking a port below 1024 on Linux or macOS, you might need superuser privileges to execute `netstat` or `lsof`. In that case, you can use `sudo`:

```bash
sudo netstat -tulpn | grep <port_number>
```

Always ensure that you have the necessary permissions to execute these commands, especially on production systems.

---------------------------

Q14 : Logic for checking whether supplied string for a script is palindrome or not? what are all the commands you will use ?
-ans :
To check whether a supplied string is a palindrome or not, you need to compare the string with its reverse. If the reversed string is the same as the original string, then it's a palindrome.

Here's a simple script in Bash that checks for a palindrome:

```bash
#!/bin/bash

# Function to check if a string is a palindrome
is_palindrome() {
    original="$1"
    reversed=$(echo "$original" | rev)
    
    if [ "$original" == "$reversed" ]; then
        echo "The string is a palindrome."
    else
        echo "The string is not a palindrome."
    fi
}

# Check if an argument is provided
if [ $# -eq 0 ]; then
    echo "Please provide a string as an argument."
    exit 1
fi

# Call the function with the supplied string
is_palindrome "$1"
```

Save this script in a file (e.g., `check_palindrome.sh`), make it executable (`chmod +x check_palindrome.sh`), and then you can use it like this:

```bash
./check_palindrome.sh "radar"
```

Replace `"radar"` with the actual string you want to check. The script will then output whether the supplied string is a palindrome or not.

Commands used in the script:

- `echo`: Prints the original string.
- `rev`: Reverses the string.
- `==`: Compares the original and reversed strings for equality.
- `if`, `else`: Conditional statements for determining if the string is a palindrome or not.

This is a basic example, and there are multiple ways to achieve the same result. Depending on your requirements and constraints, you might choose different approaches or programming languages.

-----------------

Q15 :  command to get number of lines in a file ? 
-ans :

To get the number of lines in a file, you can use the `wc` (word count) command with the `-l` option. Here's the command:

```bash
wc -l filename
```

Replace `filename` with the actual name of the file you want to count the lines for.

For example, if you have a file named `example.txt`, you would run:

```bash
wc -l example.txt
```

The output will be something like:

```
42 example.txt
```

In this example, `42` is the number of lines in the file `example.txt`. The `-l` option tells `wc` to count lines.

    grep -c ^: The grep command is a Unix/Linux command that searches for patterns in files. The -c option tells grep to count the number of matches. The ^ pattern matches the beginning of a line, so grep -c ^ counts the number of lines in a file.

Bash

grep -c ^ <filename>


Both of these commands will print the number of lines in the file to the standard output.

---------------------------------
------------------------------
--------------------------------

# ANSIBLE :

Q16 : Lets say i have 4 machines consider 1 as ansible master other 3 as nodes, what are the basic setup you need to do for ansible cluster?
-ans :

To set up an Ansible environment with one machine as the Ansible control node (master) and three machines as nodes, you need to perform the following basic setup steps:

**1. Install Ansible on the Ansible Control Node:**
   - Install Ansible on the machine designated as the Ansible control node.
   - Use the package manager specific to your operating system. For example, on a Linux machine, you might use:
     ```bash
     sudo apt-get install ansible    # For Ubuntu/Debian
     sudo yum install ansible        # For CentOS/RHEL
     ```

**2. Configure SSH for Passwordless Authentication:**
   - Ensure that the Ansible control node can SSH into the target nodes without requiring a password.
   - Set up SSH key-based authentication from the Ansible control node to each of the target nodes.
     ```bash
     ssh-keygen   # Run this on the Ansible control node
     ssh-copy-id user@node1   # Replace user and node1 with your username and node information
     ssh-copy-id user@node2
     ssh-copy-id user@node3
     ```
   - Test that you can SSH into each node without a password prompt.

**3. Create an Ansible Inventory File:**
   - Create an Ansible inventory file that lists the IP addresses or hostnames of the target nodes.
   - The inventory file is typically named `inventory` or `hosts` and may look like this:
     ```ini
     [nodes]
     node1 ansible_ssh_host=192.168.1.1
     node2 ansible_ssh_host=192.168.1.2
     node3 ansible_ssh_host=192.168.1.3
     ```

**4. Test Ansible Connection:**
   - Test Ansible's connection to the nodes using the `ansible` command.
     ```bash
     ansible -i inventory nodes -m ping
     ```
   - This should return a successful response from each node, indicating that Ansible can connect.

**5. Optional: Set Up Ansible Configuration:**
   - Customize the Ansible configuration file (`ansible.cfg`) on the Ansible control node if needed.
   - Common configurations include specifying the inventory file location, remote user, etc.

**6. Define Playbooks and Roles:**
   - Write Ansible playbooks to define tasks and roles that you want to execute on the target nodes.
   - Organize playbooks and roles in a logical directory structure.

**7. Run Ansible Playbooks:**
   - Use Ansible playbooks to deploy configurations, install packages, or perform other tasks on the target nodes.
   - Execute playbooks using the `ansible-playbook` command.

**8. Scale and Monitor:**
   - As needed, you can scale your Ansible environment by adding more nodes to the inventory file.
   - Monitor the execution of tasks, troubleshoot issues, and optimize your Ansible setup based on your requirements.

These are the basic steps to set up an Ansible environment with one control node and multiple target nodes. Depending on your specific use case, you might need to perform additional configurations or customizations.

----------------------------------

Q17 : what are ansible roles? why we need ansible roles? have you worked on ansible galaxy?
-ans :
**Ansible Roles:**

An Ansible role is a reusable and self-contained unit of automation that bundles together tasks, variables, templates, and other Ansible elements. Roles are used to organize and structure Ansible playbooks, making them more modular, maintainable, and scalable. A role encapsulates a specific functionality or role (e.g., web server, database server, monitoring) and can be shared and reused across different projects.

**Key Components of an Ansible Role:**
1. **Tasks:** The main automation logic, written in YAML, that defines what the role does.
2. **Variables:** Parameters and configuration settings for the role.
3. **Templates:** Jinja2 templates used to generate configuration files dynamically.
4. **Handlers:** Tasks that are triggered by events and are typically used to restart services after a configuration change.
5. **Defaults:** Default variable values for the role.
6. **Meta:** Metadata for the role, including dependencies on other roles.

**Why We Need Ansible Roles:**

1. **Modularity and Reusability:** Roles provide a modular and reusable way to structure automation code. You can develop roles independently and reuse them across different projects.

2. **Organization:** Roles help organize and structure playbooks, making them more readable and maintainable. Each role encapsulates a specific functionality, making the playbook easier to understand.

3. **Code Sharing:** Roles can be shared with the community through platforms like Ansible Galaxy. This promotes collaboration and allows users to leverage pre-built roles for common tasks.

4. **Versioning:** Roles can have versions, enabling you to use a specific version of a role to ensure consistency across deployments.

5. **Dependency Management:** Roles can depend on other roles, allowing you to define a hierarchy of roles that represent different layers of functionality (e.g., base OS configuration, application installation, etc.).

**Ansible Galaxy:**

Ansible Galaxy is a web-based platform for sharing, discovering, and collaborating on Ansible roles. It is a central repository where Ansible roles can be published, making it easy for users to find and reuse roles created by others. Roles on Ansible Galaxy can be installed and used in playbooks directly.

**Key Features of Ansible Galaxy:**

1. **Role Sharing:** Allows users to share their Ansible roles with the community.
2. **Search and Discovery:** Provides a search functionality to find roles based on keywords, categories, or maintainers.
3. **Role Installation:** Supports easy installation of roles directly from Galaxy using the `ansible-galaxy` command.
4. **Versioning:** Roles can have multiple versions, allowing users to choose a specific version when installing.

**Role Usage Example:**

```yaml
---
- hosts: servers
  roles:
    - geerlingguy.apache
    - geerlingguy.mysql
```

In this example, the playbook uses two roles from Ansible Galaxy: `geerlingguy.apache` for configuring an Apache web server and `geerlingguy.mysql` for configuring a MySQL database server.

Roles enhance the maintainability, reusability, and collaboration aspects of Ansible playbooks, making automation workflows more efficient and scalable.

------------------------------------

Q18 : Have you worked on ansible galaxy ? what is ansible galaxy ?
-ans :

Yes, I have worked with Ansible Galaxy. Ansible Galaxy is a web-based platform and command-line tool that serves as a central repository for sharing, discovering, and collaborating on Ansible roles. Roles, in the context of Ansible, are units of automation that bundle together tasks, variables, templates, and other components necessary to perform a specific function or configuration.

Key aspects of Ansible Galaxy include:

1. **Role Sharing:** Ansible Galaxy allows users to share their Ansible roles with the broader community. This facilitates collaboration and enables users to leverage pre-built roles for common tasks rather than starting from scratch.

2. **Search and Discovery:** Users can search for roles based on keywords, categories, or maintainers. This search functionality makes it easy to find roles that suit specific automation requirements.

3. **Role Installation:** The `ansible-galaxy` command-line tool is used to install roles from Ansible Galaxy. This makes it straightforward for users to integrate roles into their playbooks.

4. **Versioning:** Roles on Ansible Galaxy can have multiple versions. This versioning system allows users to choose a specific version of a role that meets their compatibility and feature requirements.

Working with Ansible Galaxy typically involves the following steps:

- **Installing Roles:** Use the `ansible-galaxy install` command to install roles from Ansible Galaxy. For example:
  ```bash
  ansible-galaxy install username.rolename
  ```

- **Integrating Roles in Playbooks:** Reference the installed roles in Ansible playbooks to leverage their functionality. For example:
  ```yaml
  ---
  - hosts: servers
    roles:
      - username.rolename
  ```

- **Contributing Roles:** Users can contribute their own roles to Ansible Galaxy, making them available to the community. This involves publishing the role on Ansible Galaxy and following best practices for documentation.

In summary, Ansible Galaxy serves as a hub for sharing and discovering Ansible roles, promoting collaboration, and accelerating automation workflows by allowing users to build on the work of others.

-------------------------

Q19 :  What are ansible facts?
-ans :
In Ansible, facts are variables that store information about the target systems, such as network details, hardware information, operating system properties, and more. Ansible collects these facts automatically when a playbook is executed on a target host, and you can use these facts in your playbooks to make them more dynamic and adaptable to different environments.

Key points about Ansible facts:

1. **Automatic Collection:** Ansible automatically collects facts about the target system when a playbook runs. This collection includes a wide range of information, such as system architecture, IP addresses, installed software, etc.

2. **Stored in Variables:** Collected facts are stored in variables and can be accessed within playbooks. These variables follow a specific naming convention, such as `ansible_<fact_name>`.

3. **Dynamic and Contextual:** Facts provide dynamic and contextual information about the target systems. This allows playbooks to adapt to the specific characteristics of each system.

4. **Examples of Facts:** Common facts include `ansible_distribution` (the Linux distribution), `ansible_os_family` (the operating system family), `ansible_hostname` (the hostname of the target system), and many more.

**Example Playbook Using Ansible Facts:**

```yaml
---
- name: Display System Information
  hosts: my_servers
  gather_facts: true   # This is the default, but you can explicitly enable or disable fact gathering

  tasks:
    - name: Print Operating System
      debug:
        var: ansible_distribution

    - name: Print Hostname
      debug:
        var: ansible_hostname
```

In this example, the playbook collects facts about the target system and prints the operating system and hostname using the `debug` module.

To view all collected facts, you can use the `setup` module in a playbook:

```yaml
---
- name: Display All Facts
  hosts: my_servers
  gather_facts: true

  tasks:
    - name: Display All Facts
      setup:
```

This playbook will output a comprehensive list of facts for each target host.

Ansible facts are system data and properties that Ansible gathers about the target nodes it connects to. These facts provide information about the hardware, software, and configuration of the nodes, which Ansible can use to make decisions about tasks and configurations.

Examples of Ansible facts:

    IP address
    Operating system
    CPU architecture
    Memory usage
    Installed software
    User accounts
    Network configuration

Ansible facts are stored in a JSON dictionary that is accessible to Ansible playbooks and templates. This allows you to use facts to dynamically configure your nodes based on their specific characteristics.
In summary, Ansible facts provide valuable information about the target systems and enhance the flexibility and adaptability of Ansible playbooks.


------------------------

Q20 : Can we have windows machine as ansible master? as node?have you worked on any windows modules? can you list few?any extra configuration do we need to do ?
-ans :

Yes, Ansible supports managing both Windows and Linux machines, and you can have a Windows machine serve as both the Ansible control node (master) and as a managed node. Ansible achieves this through its WinRM (Windows Remote Management) protocol for communication with Windows machines.

**Windows as Ansible Control Node:**
- Yes, you can have the Ansible control node running on a Windows machine. However, it's more common to use Linux or macOS as the control node.

**Windows as Ansible Managed Node:**
- Yes, Ansible can manage Windows machines as nodes. You need to enable and configure WinRM on the Windows machines for Ansible to communicate with them.

**Windows Modules:**
Ansible provides specific modules designed to work with Windows systems. Some common Windows modules include:
1. `win_command`: Run Windows commands.
2. `win_shell`: Run PowerShell commands on Windows.
3. `win_copy`: Copy files to Windows machines.
4. `win_file`: Manage files and directories on Windows.
5. `win_service`: Manage services on Windows.
6. `win_updates`: Manage Windows updates.

**Extra Configuration for Windows Nodes:**
To use Ansible with Windows nodes, you need to perform the following additional configurations:

1. **Enable WinRM on Windows:**
   - WinRM must be enabled on the Windows machines.
   - Run the following PowerShell command on each Windows machine to enable WinRM:
     ```powershell
     winrm quickconfig -q
     ```

2. **Firewall Configuration:**
   - Ensure that the Windows Firewall allows WinRM traffic. You might need to open the WinRM port (default is 5985) on the Windows firewall.

3. **WinRM Authentication Configuration:**
   - Configure WinRM to allow basic authentication or, for more secure setups, configure Kerberos authentication.
   - Example for allowing basic authentication:
     ```powershell
     winrm set winrm/config/service/Auth @{Basic="true"}
     ```

4. **SSL Configuration (Optional):**
   - For enhanced security, you can configure WinRM to use SSL. This involves obtaining and configuring SSL certificates.

**Example Inventory File:**
```ini
[windows]
windows-server ansible_host=192.168.1.100 ansible_user=administrator ansible_password=your_password ansible_connection=winrm ansible_winrm_server_cert_validation=ignore
```

In this example, replace `192.168.1.100` with the actual IP address or hostname of your Windows machine. Provide the appropriate `ansible_user` and `ansible_password` for authentication.

**Example Playbook:**
```yaml
---
- name: Example Windows Playbook
  hosts: windows
  gather_facts: false   # Facts gathering is not supported on Windows
  tasks:
    - name: Run PowerShell Command
      win_shell: Get-Service
```

This simple playbook runs a PowerShell command (`Get-Service`) on the Windows machine.

In summary, Ansible can seamlessly manage both Windows and Linux machines, and additional configurations are required for WinRM communication on Windows nodes. The Ansible documentation provides detailed guidance on working with Windows: [Ansible Windows Guides](https://docs.ansible.com/ansible/latest/user_guide/windows.html).


------------------------
------------------------
-------------------------

# DOCKER :


Q21 : Have you worked on docker save , docker load ?
-ans :

Yes, I have worked with `docker save` and `docker load`. These commands are used for saving and loading Docker images, allowing you to export images to a tarball file and import them back into Docker.

1. **`docker save`:**
   - The `docker save` command is used to save one or more Docker images to a tarball file. This is useful when you want to share images with others or move them between environments.

   **Syntax:**
   ```bash
   docker save [OPTIONS] IMAGE [IMAGE...]
   ```

   **Example:**
   ```bash
   docker save -o my_images.tar.gz ubuntu:latest nginx:latest
   ```
   - This command saves the `ubuntu:latest` and `nginx:latest` images to a tarball file named `my_images.tar.gz`.

2. **`docker load`:**
   - The `docker load` command is used to load Docker images from a tarball file back into the local Docker environment. This is helpful when you have received a tarball file containing images and want to use those images on your system.

   **Syntax:**
   ```bash
   docker load [OPTIONS]
   ```

   **Example:**
   ```bash
   docker load -i my_images.tar.gz
   ```
   - This command loads images from the `my_images.tar.gz` tarball file into the local Docker environment.

These commands are particularly useful in scenarios where you need to transfer Docker images between different environments, such as moving images from a development environment to a production environment or sharing custom images with team members.

**Additional Tips:**
- When using `docker save`, the `-o` or `--output` option specifies the output file.
- When using `docker load`, the `-i` or `--input` option specifies the input file.

**Example Workflow:**
1. On the machine with the source Docker environment:
   ```bash
   docker save -o my_images.tar.gz ubuntu:latest nginx:latest
   ```

2. Transfer the `my_images.tar.gz` file to the destination machine.

3. On the machine with the destination Docker environment:
   ```bash
   docker load -i my_images.tar.gz
   ```

This workflow ensures that the same set of images is available in the destination environment as was saved in the source environment.

---------------------------


Q22 :  Have you worked on multi-stage dockerfile and why we need that?
-ans :

Yes, I have worked with multi-stage Dockerfiles. Multi-stage builds in Docker allow you to create smaller and more efficient Docker images by using multiple build stages within a single Dockerfile. This feature is particularly useful when you need to compile code, build artifacts, or perform other tasks during the Docker image build process.

**Key Reasons for Using Multi-stage Dockerfiles:**

1. **Reducing Image Size:**
   - Multi-stage builds help reduce the final size of Docker images. In a typical build scenario, intermediate build artifacts, development dependencies, and build tools are included in the image. With multi-stage builds, you can separate the build environment from the runtime environment, resulting in a smaller and more focused final image that only contains the necessary runtime components.

2. **Isolation of Build Tools:**
   - The build tools and dependencies required for compiling or building an application are isolated in the build stage. Once the build is complete, only the necessary artifacts are copied to the final stage. This helps keep the production image clean and free from unnecessary build dependencies.

3. **Improved Security:**
   - By separating the build and runtime environments, you reduce the attack surface of the final image. The runtime image only includes the essential components needed to run the application, minimizing potential security risks associated with unnecessary tools or libraries.

4. **Clarity and Readability:**
   - Multi-stage builds improve the clarity and readability of Dockerfiles. Each stage in the Dockerfile represents a logical step in the build process, making it easier for developers and maintainers to understand and modify the build process.

**Example of a Multi-stage Dockerfile:**

```Dockerfile
# Build stage
FROM golang:1.16 AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp

# Final stage
FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/myapp .
CMD ["./myapp"]
```

In this example, the first stage uses a Golang base image to build the application, and the second stage uses a minimal Alpine Linux image to run the compiled application. The `--from=builder` syntax is used to copy artifacts from the builder stage to the final stage.

By adopting multi-stage builds, you achieve a streamlined and efficient Docker image that only contains what is necessary for running the application in a production environment.

--------------------------

Q23 : Lets say i have container which is attached with a volume, if container crashes what happens to volume?
-ans :

If a container crashes, the associated volume in Docker remains intact. Docker volumes are designed to persist data independently of the container's lifecycle. Here are the key points to understand:

1. **Volume Lifecycle:**
   - Volumes in Docker exist outside the lifecycle of containers. They are created separately and persist even if the associated container stops or crashes.

2. **Data Persistence:**
   - The purpose of volumes is to provide a way for containers to share and persist data. Even if a container crashes or is stopped, the data stored in the volume remains accessible.

3. **Volume Cleanup:**
   - Docker does not automatically remove volumes when a container exits or is removed. Volumes must be explicitly deleted using the `docker volume rm` command.

4. **Recovery:**
   - If a container crashes and is subsequently restarted or replaced, the new container can still access the data in the volume. As long as the volume is not removed, the data is available for other containers to use.

**Example:**
```bash
# Create a volume
docker volume create mydata

# Run a container with the volume
docker run -d --name mycontainer -v mydata:/app myimage

# If the container crashes or is stopped, the volume persists
docker stop mycontainer

# Start a new container with the same volume
docker run -d --name newcontainer -v mydata:/app myimage
```

In this example, even if `mycontainer` crashes or is stopped, the `mydata` volume remains intact. The `newcontainer` can then use the same volume to access the persisted data.

Remember that volumes are a separate entity in Docker, providing a way to manage and persist data independently of containers. This decoupling ensures data integrity and persistence across the lifecycle of containers.

---------------------------

Q24 : Can you copy a file from local to running containers ?
-ans :


Yes, you can copy a file from the local machine to a running container using the `docker cp` command. The `docker cp` command allows you to copy files or directories between a container and the local filesystem.

Here's the basic syntax:

```bash
docker cp <local_file_or_directory> <container_id_or_name>:<destination_path_inside_container>
```

- `<local_file_or_directory>`: The path to the file or directory on the local machine.
- `<container_id_or_name>`: The ID or name of the running container.
- `<destination_path_inside_container>`: The path inside the container where you want to copy the file.

For example, if you have a file named `example.txt` on your local machine and you want to copy it to a running container with the ID `container123` in the `/app` directory inside the container, you would run:

```bash
docker cp example.txt container123:/app
```

After executing this command, the `example.txt` file will be copied into the `/app` directory within the running container.

It's important to note that this method copies the file into the container, but changes made to the file inside the container will not affect the original file on the local machine, and vice versa. If you need to synchronize files between the local machine and a container, you might want to consider using volumes or other mechanisms based on your specific use case.



---------------------
-------------------
====================

### Kubernetes :


Q25 : what is init container and side-car container?can you give simple scenario where we use these conatiners?

- ans :
Init containers and sidecar containers are two common patterns used in Kubernetes to enhance the functionality of pods. 

1. **Init Containers**:
   Init containers are designed to run before the main container in a pod starts. They are useful for performing initialization tasks such as setup, configuration, and data preparation. Init containers are perfect for scenarios where you need to ensure some conditions are met before the main application starts. They are typically used to:

   *  Prepare the environment for the main application container, such as by creating files or directories, or installing dependencies.
   *  Wait for external services to become available.
   *  Run health checks to ensure that the environment is ready for the main application container to start.

 Here's a simple scenario:

   *Scenario*:
   - Imagine you have a web application running in a pod, and it relies on a configuration file that must be generated by a separate process before the application starts. You can use an init container for this task. The init container can generate the configuration file and place it in a shared volume. Once the init container successfully completes its task, the main application container can start, read the configuration file, and run with the desired settings.   or
   - One use for init containers is to bootstrap Appian with RDBMS/JDBC drivers not included in the Webapp Docker image (for example, MySQL or IBM Db2).
   - A web application that needs to download a large configuration file from a remote server before starting.
   - A database application that needs to wait for the database server to become available before starting.
   - A microservices application that needs to run a health check on all of its dependencies before starting.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: init-container
      image: busybox
      command: ['sh', '-c', 'wget -O /config/config.yaml http://config-server/config.yaml']
      volumeMounts:
        - name: config-volume
          mountPath: /config
    - name: main-container
      image: myapp-image:latest
      volumeMounts:
        - name: config-volume
          mountPath: /app/config
  volumes:
    - name: config-volume
      emptyDir: {}


```

3. **Sidecar Containers**:
   Sidecar containers are additional containers that run alongside the main application container in the same pod. They are used to extend or enhance the functionality of the main container without modifying the application's code.They are typically used for tasks such as:

    * Logging and monitoring
    * Caching
    * Load balancing
    * Service discovery
    * Security

 Here's a simple scenario:

   *Scenario*:
    - Suppose you have a microservices architecture where each service emits logs, and you want to centralize log collection and forwarding to a logging service like Elasticsearch or Fluentd. You can use a sidecar container for this. The main application container generates logs, while the sidecar container collects these logs and sends them to the logging service. This keeps your application container focused on its primary task, while the sidecar container handles the logging responsibilities.
   

  - A web application that needs to use a caching service to improve performance.
  - A database application that needs to use a load balancer to distribute traffic across multiple replicas.
  - A microservices application that needs to use a service discovery service to locate its dependencies.
  - A web application that needs to use a security sidecar to implement authentication and authorization.


```yaml

apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: main-container
      image: myapp-image:latest
      ports:
        - containerPort: 8080
      # Your main application container configuration goes here
    - name: log-forwarder
      image: log-forwarder-image:latest
      # Configuration for log forwarding goes here

```
In summary, init containers are primarily used for setup and initialization tasks that need to be completed before the main application container starts, while sidecar containers are used to enhance the functionality of the main container by running alongside it and performing tasks like logging, monitoring, or data synchronization. These patterns help keep pods clean, modular, and easier to manage in a container orchestration environment like Kubernetes.


-------------

Q26 : which one is default deployment strategy? how it works?

-ans :

The default deployment strategy in Kubernetes is a "Rolling Update." A Rolling Update gradually replaces instances of the previous version of an application with instances of the new version while maintaining a specified number of healthy replicas during the update process. Here's how it works:

1. **Replica Sets**: Kubernetes uses Replica Sets to ensure that a specific number of pod replicas are running at all times. When you create a Deployment, it manages a Replica Set for you.

2. **Updating the Deployment**:
   - When you want to update your application, you make changes to the Deployment configuration, typically by updating the container image version of your pods.
   - Kubernetes then creates a new Replica Set with the updated configuration while keeping the old one intact.

3. **Scaling Down the Old Replica Set**: The Rolling Update strategy ensures a controlled transition between the old and new versions. It gradually scales down the old Replica Set while simultaneously scaling up the new one. This gradual process avoids sudden disruptions.

4. **Readiness Probes**: Kubernetes uses readiness probes to determine if a new pod is ready to serve traffic. It won't start scaling down pods in the old Replica Set until the new pods are ready, ensuring there's a sufficient number of ready replicas running your application even during the update.

5. **Monitoring and Completion**: Kubernetes continuously monitors the update process, ensuring the desired number of replicas for the new version are running, and the old version is scaled down gradually.

6. **Rollback**: If any issues are detected during the update process, Kubernetes can automatically roll back to the previous version by scaling down the new Replica Set and scaling up the old one.

The Rolling Update strategy offers several benefits:
- **Minimized Downtime**: It allows you to update your application without significant downtime, as new replicas are gradually introduced while old ones are retired.
- **Reduced Risk**: It enables you to test the new version of your application before fully deploying it, reducing the risk of introducing new bugs or issues.
- **Flexibility**: You can configure the speed of the update, making it as gradual or fast as needed.

For those new to Kubernetes, the Rolling Update deployment strategy is recommended, as it is the default strategy and provides a straightforward and controlled approach to application updates.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp-container
        image: myapp-image:v2  # Update this to your new image version
        ports:
        - containerPort: 80
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  minReadySeconds: 5

```
-----------------

Q27 :  command to check the container logs in pod?
-ans :

To check the container logs in a pod in Kubernetes, you can use the `kubectl logs` command. Here's the basic syntax:

```shell
kubectl logs <pod_name> [-c <container_name>]
```

- `<pod_name>`: Replace this with the name of the pod for which you want to view the logs.
- `-c <container_name>` (optional): If the pod has multiple containers, you can specify the container name to view logs for a specific container within the pod. If the pod has only one container, this flag is not required.

Here are a few examples:

1. To check the logs for a container in a pod with a single container:
   
   ```shell
   kubectl logs my-pod
   ```

2. To check the logs for a specific container in a pod with multiple containers:

   ```shell
   kubectl logs my-pod -c my-container
   ```

The `kubectl logs` command will display the logs from the specified container in the pod directly in your terminal. If you need to follow the logs in real-time (similar to the `tail -f` command), you can use the `-f` flag:

```shell
kubectl logs -f <pod_name> [-c <container_name>]
```

This will continuously stream the logs to your terminal as new log entries are generated.

Remember to replace `<pod_name>` and `<container_name>` with the actual names of your pod and container.

You can also use the --all-containers=true flag to print the logs for all containers in the pod, even if they are not running:

```kubectl logs <pod-name> --all-containers=true```

events ` kubectl get events --field-selector involvedObject.name=<pod-namw>`

--------------



Q28 : what are the types of services present in kubernetes?
-ans :

Kubernetes offers several types of services to expose applications and manage network communication within a cluster. The common types of services in Kubernetes are:

1. **ClusterIP**:
   - **ClusterIP** services provide internal network communication within the cluster. They expose the service on a cluster-internal IP address, allowing other pods within the cluster to access it. These services are not accessible from outside the cluster.
```yaml

apiVersion: v1
kind: Service
metadata:
  name: myapp-clusterip-service
spec:
  selector:
    app: myapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080


```

2. **NodePort**:
   - **NodePort** services expose the service on a static port on each node's IP address. They make the service accessible from outside the cluster. When traffic is directed to a node's IP and the defined port, the service forwards it to the appropriate pod.
   
```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-nodeport-service
spec:
  selector:
    app: myapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: NodePort


```


3. **LoadBalancer**:
   - **LoadBalancer** services are used to expose services to the outside world through cloud provider-specific load balancers. They distribute external traffic to the pods behind the service, making it suitable for scenarios where you need to load balance and provide high availability for external access.
   
```yaml

apiVersion: v1
kind: Service
metadata:
  name: myapp-loadbalancer-service
spec:
  selector:
    app: myapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: LoadBalancer

```



4. **ExternalName**:
   - **ExternalName** services provide a way to map a service to a DNS name. These services do not have selectors or endpoints but instead redirect DNS queries to a specified external DNS name.
```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-externalname-service
spec:
  externalName: myapp.example.com


```

5. **Headless**:
   - A **Headless** service, when created with the `ClusterIP: None` setting, does not allocate a cluster-internal IP or provide load balancing. It is used for scenarios where you need direct DNS-based pod-to-pod communication within a service without a single entry point.
```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-headless-service
spec:
  clusterIP: None
  selector:
    app: myapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080


```

6. **Ingress**:
   - An **Ingress** resource is not exactly a service, but it manages external access to the services in your cluster. Ingress controllers can be used to configure rules for routing external traffic to specific services based on HTTP or HTTPS routes.

```yaml

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myapp-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: myapp-service
            port:
              number: 80


```

These services are essential for managing networking and making your applications accessible within a Kubernetes cluster and, when needed, from external sources. The choice of service type depends on your application's requirements and the desired access patterns.

--------------------


Q29 : What is the link between pod and service?

-ans :

Pods and services in Kubernetes are closely related and work together to ensure network communication within the cluster. Here's the link between pods and services:

1. **Pods**:
   - A **Pod** is the smallest deployable unit in Kubernetes. It can contain one or more containers that are tightly coupled and share the same network namespace. Containers within a pod can communicate with each other over the localhost, making them suitable for running co-located components of an application.

2. **Services**:
   - **Services** are Kubernetes resources that provide a stable, network-internal endpoint to access a group of pods. They abstract the underlying pod instances, allowing you to connect to a service rather than individual pods. Services provide a way to load balance traffic across multiple pods and ensure that network requests are routed to healthy pods.

The link between pods and services is established through **label selectors** and **service endpoints**:

- **Label Selectors**: Pods are labeled with key-value pairs, and services are configured with label selectors to identify the pods they should target. The label selectors define which pods are part of a service. For example, a service can target all pods labeled with `app=web`.

- **Service Endpoints**: When you create a service with specific label selectors, Kubernetes dynamically discovers the pods that match those labels and forms a list of **endpoints**. These endpoints are the individual pod IP addresses and ports that belong to the service. The service maintains this list and automatically updates it as pods are created or terminated.

Here's how the relationship works:

1. You create one or more pods that provide a specific application or service.
2. You label these pods with appropriate labels, allowing you to group them based on their purpose or characteristics.
3. You create a service that targets pods with specific labels.
4. The service maintains a list of endpoints (pod IP addresses and ports) based on the selected label criteria.
5. When other pods or external clients need to communicate with the application, they use the service's ClusterIP or DNS name. The service forwards incoming traffic to one of the available endpoints (pods).

This decouples the pods from direct exposure to the network and provides a level of abstraction and load balancing. Services help in load balancing incoming traffic and ensuring that network requests are routed to healthy pods, even when the pod instances change due to scaling or updates.


A pod is a group of one or more containers, with shared storage and network resources, that are deployed together on a Kubernetes node. A service is an abstraction which defines a logical set of Pods running somewhere in your cluster, that all provide the same functionality.

Services are linked to pods in two ways:

  1. Label selector: A service uses a label selector to identify the pods that it should proxy traffic to. The label selector can be based on any label that is applied to the pods.
  2. Endpoints: A service is backed by a set of endpoints, which are the actual pods that the service will proxy traffic to. The endpoints are discovered by the Kubernetes service proxy, which is responsible for load balancing traffic to the pods.

When a client sends traffic to a service, the Kubernetes service proxy intercepts the traffic and forwards it to one of the pods that is backing the service. The service proxy uses a load balancing algorithm to distribute traffic evenly across the pods.

The link between pods and services is essential for running reliable and scalable applications on Kubernetes. Services allow you to expose your application to the outside world without having to worry about managing the individual pods that are backing the service. Services also provide load balancing and failover capabilities, which ensure that your application is always available, even if some of the pods that are backing it fail.

Here is an example of how a service is linked to pods:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```
This service will proxy traffic to all pods that have the label app: my-app. The service will listen on port 80 and forward traffic to port 80 on the pods.

To deploy this service, you would run the following command:

`kubectl apply -f service.yaml`

Once the service is deployed, you can access it from outside the cluster using the service's IP address. The Kubernetes service proxy will load balance traffic to the pods that are backing the service.
Benefits of linking pods and services

Linking pods and services has a number of benefits, including:

  1. Abstraction: Services provide an abstraction layer that hides the complexity of managing individual pods. This makes it easier to develop and deploy applications on Kubernetes.
  2. Load balancing: Services provide load balancing capabilities, which distribute traffic evenly across the pods that are backing the service. This improves the performance and reliability of your application.
  3. Failover: Services also provide failover capabilities. If a pod fails, the service will continue to proxy traffic to the remaining pods. This ensures that your application is always available, even if some of the pods that are backing it fail.
  4. Scalability: Services make it easy to scale your application up or down. You can simply add or remove pods from the service, and the service will automatically update its endpoint list. This makes it easy to scale your application to meet the changing demands of your users.
