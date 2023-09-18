 ## Devops Interview questions | Devops Telephonic interview - 1 ( Mock Interview ) 
 
* Mock : https://www.youtube.com/watch?v=i7YJesoeWFI&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq
* Ans : https://www.youtube.com/watch?v=5w8qVukxXXY&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=9
 
---------

Q1 : Brief me all the tools you have worked on and daily activites you used to work on ?
- ans :


__________

Q2 : so you worked on git right , so it only push , pull or you have also worked on admin activity ?
- ans :

I have worked mostly on git push and pull , clone , fetch , as I worked as devops engineer, most of the admin activities were performed by the developer or the repo admins they used to perform admin activities like access control, repository management, branching strategies, code reviews , issue tracking, backup n recovery, git maintenance, compliance and security, got hooks . 

I have worked on GitHub webhook, whenever there's a commit a jenkins job used to trigger , and I have created pat token for the Authorization by selecting the correct permissions. GitHub webhook is nothing but an api request. It send tha data i.e http post and send some json payload to the endpoint we have configured. There are various api protocols like grpc , http, UDP , TCP here it uses http protocol for the communication and here it performance two way handshake let's suppose it sends some data to jenkins, jenkins will reply back as the data has been received and triggers the job by fetching the changs. 


I have also migrated the GitHub repo to code commit. Here we need to create a repo in code commit then need to clone in the local laptop or whatever machine we are using, while cloning we may need some permission to access the code commit repo for this we can use iam role attached to vm in case our machine is ec2 or we can create AWS iam user by giving proper set of permissions. Then we can clone the code commit repo we also need to clone gitrepo if the repo is private we may need pat token then update the config file i.e located in .git folder where we need to update origin url or we can use the command to update origin url , a better way to use the command so we can track the changes by AWS Cloudwatch agent or any other monitoring agent if we are using.

After updating the origin url we can push the repo to code commit here we need to make sure every branch is pushed. We can use command to push all branches or if we have so many branches we can use a script to do that aswell , script may include a loop to push the branch one by one. 

In azure the migration is very simple as git is owned by Microsoft only we just need to enter the git url and pat token and by using import option the whole git repo will be migrated.


 For Oracle also we need to follow the steps like AWS. 


when setting up webhooks or migrating repositories, it's crucial to consider security measures. For GitHub webhooks, using a secret token and verifying the HMAC signature of incoming payloads helps ensure data authenticity. also the pat token should be stored in key vaults of the respective cloud services AWS Azure Oracle considering the sensitivity. and while configuring the roles of giving permissions we should follow the rbac and least privileged.

__________
---------

Q3 : Why we need git and what it makes unique from other tools like SVN ?

- ans :

Git vs SVN

Git and svn are both version controls systems howvever Git is more vcs and SVN is RCS,

Git operates locally, developers clones the main repo and can make changes or code without connecting to the main repo. they only need to connect when they are commiting the changes to the main repo or pushing the changes. this helps to limit the network traffic which may reduce teh cost if we are running the servers on the cloud i.e ingress charges. However SVN has limited offline capabilities

By using git we can avoid the single point of failure, as the copy will be available in dev laptop and in case the repo is deleted from github we can restore ( if we are restoring from the laptop we need to have all the branches) the SVN can be a single point of failure unless we have configured backup 

⚫in git dev can work independtly rather than on centralized manner like svn, and if any merge conflict arises it can be handeled easily.

⚫ svn can be better for RBAC in git we cant enable acces to some code files like svn does however it can be possible with 3rd party plugin but wen need to make sure there is no CVES attached.

Selecting Git and svn depends on how much granular security we needs and no. of parallel contributors.

codecommit doesnot supports SVN, we need to migrate svn to git then we can push to codecommit, Azures repos supports SVN and Git both i.e DVCS and CVCS, OCI repositories



----------
-----------

Q4 : so lets say you have a scenario, i have a maven repo cloned on to my local, did some changes and i have build the code like mvn install now target folder will be generated, so now when i do git operations like git add , git commit or any other git operation target folder should not be considered, how would you achieve the same ?

- ans :

We can use the .gitignore file if we need some files which are not to be pushed to main repository.



we can add file or folder names in gitignore file, if we are using VS Code this file will be generated automatically and content of gitignnore depends on project we are creating. or

there are various templates are also available on the ietrnet

this file is located in the root firectory of the repo and it is a plain text file ans it supports the regex and pattern match

if our gitignore file is long or we are in some other folder we can use 'git check-ignore -v path/to/ignored/file to chewck if the file is in gitignore or not


--------
--------


Q5 : Difference between git pull and git fetch ?

- ans :


Git fetch vs git pull

Git fetch gives the information of new changes from the remote repo without merging in thw current branch and the data is tored in .git we can revew the changes and git merge can be done and while using git fetc there are less chances of merge conflict because we are aware what previous changes has been done and depending on that git merge can be done

however

git pull is addition of git fetch and git merge git pull brings all the changes made to remote repo and merges in our current branch and our repository will be updated, In this case merge conflict may arise 1 there are changes at the same place.

we can say git fetch is the safe and non destructive of these 2 commands


---------
---------

Q6 : How to clone specific branch in  git ?

- ans :


To clone a specific branch we can use -b flag, or we can also use ` git clone --single-branch --branch < branch name> <remote repo url> `

if we use only --single-branch by default it will clone master or main only and for specific branch we need to use --branch, we can use --depth to save the bandwith

there are other ways as well like cloning the repo with all branches and checkout to specific branch however that doesnt answer the question to clone specific branch only.

-----
-----

-------------------------

Q7 : When i issue mvn install what all things happen in background ?
- ans :

When you issue the `mvn install` command in a Maven project, several things happen in the background to build and install the project. Maven is a build automation tool used primarily for Java projects, and `mvn install` is a common command used to build and install a project into your local Maven repository. Here's a high-level overview of what happens when you run `mvn install`:
On a mvn install, it frames a dependency tree based on the project configuration pom. xml on all the sub projects under the super pom. xml (the root POM) and downloads/compiles all the needed components in a directory called . m2 under the user's folder.


1. **Parsing the Project**: Maven starts by parsing the `pom.xml` file in your project's root directory. This XML file contains project metadata, dependencies, plugins, and build instructions. Maven checks to make sure that the POM file is well-formed and contains all of the required information.

2. **Dependency Resolution**: Maven checks the local repository (usually located at `~/.m2/repository`) to see if any of the project's dependencies are already present. If not, it proceeds to download them from remote repositories specified in the `pom.xml` (such as Maven Central or a corporate repository). Maven downloads all of the project's dependencies from the remote Maven repositories to the local Maven repository.

3. **Compiling Source Code**: Maven compiles the Java source code in your project, typically located in the `src/main/java` directory. It also compiles any test code located in the `src/test/java` directory. Maven compiles the project's Java source code into Java bytecode (bytecode is the machine code that is executed by the Java Virtual Machine).

4. **Running Tests**: If you have defined unit tests in your project (usually located in the `src/test/java` directory), Maven will execute these tests. If any tests fail, the build process will typically stop, and the project won't be installed. Maven runs the project's unit tests to ensure that the code is working as expected.

5. **Packaging**: After a successful compilation and testing phase, Maven packages your project into a specific format, depending on the packaging type defined in the `pom.xml`. Common packaging types include JAR (Java Archive), WAR (Web Application Archive), and others. Maven packages the project's compiled bytecode and other resources into a JAR (Java Archive) file.

6. **Installing in the Local Repository**: The built artifact (e.g., JAR or WAR file) is installed in your local Maven repository. By default, this repository is located in `~/.m2/repository`. This allows other Maven projects on your machine to depend on and use the artifact. Maven installs the project's JAR file to the local Maven repository.

7. **Cleaning Up**: Maven performs some cleanup tasks, like deleting temporary build files and directories created during the build process.

8. **Reporting**: Maven generates reports on the build process, including test results and other useful information. These reports are typically stored in the `target` directory of your project.

9. **Plugin Execution**: During the build process, various Maven plugins specified in the `pom.xml` file are executed. These plugins can perform additional tasks, such as generating documentation, code analysis, or custom build steps.

10. **Build Success or Failure**: Finally, Maven reports whether the build was successful or if any errors occurred during the process. If successful, your project's artifact is now available in your local repository for other projects to use.

Keep in mind that Maven's behavior can be customized extensively through configuration in the `pom.xml` file, so the specific actions taken during the `mvn install` command can vary from project to project. However, the general sequence of dependency resolution, compilation, testing, packaging, and installation remains consistent. The mvn install command can be used to install both single-module and multi-module Maven projects. For multi-module projects, Maven will install the JAR file for each module to the local Maven repository.

In addition to the above steps, Maven also performs a number of other tasks in the background, such as:

    Managing the project's build lifecycle
    Generating documentation
    Reporting on the build progress

The specific tasks that Maven performs will depend on the configuration of the project POM file.
Example

The following example shows how to use the mvn install command to install a single-module Maven project:

mvn install

This command will compile the project's source code, run the unit tests, package the project, and install the project's JAR file to the local Maven repository.

The following example shows how to use the mvn install command to install a multi-module Maven project:

mvn clean install -am

This command will clean the build artifacts for all of the project's modules, compile the source code for all of the modules, run the unit tests for all of the modules, package all of the modules, and install all of the modules' JAR files to the local Maven repository.
Why is mvn install useful?

The mvn install command is useful for a number of reasons, including:

    It automates the process of building and installing Maven projects.
    It ensures that all of the project's dependencies are downloaded and installed correctly.
    It provides a consistent way to build and install Maven projects on different platforms.
    It allows Maven projects to be easily shared with other developers.

 

```
clean  :   Delete target directory.
validate   :    Validate if the project is correct.
compile   :   Compile source code, classes stored in target/classes.
test   :   Run tests.
package   :   Take the compiled code and package it in its distributable format, e.g. JAR, WAR.
verify   :    Run any checks to verify the MVN package is valid and meets quality criteria.
install   :    Install the package into the local repository.
deploy   :   Copies the final MVN package to the remote repository.
```




-----
-------

Q8 : Do you know what is .m2 folder ?
- ans :

Yes, I can provide information about the `.m2` folder. The `.m2` folder is a directory that is typically found in a user's home directory (e.g., `C:\Users\<username>` on Windows or `/Users/<username>` on macOS and Linux). This folder is created and used by Apache Maven, a popular build automation and project management tool primarily used for Java projects.

Here's what the `.m2` folder contains:

1. **Repository**: The most important subdirectory within `.m2` is the `repository` directory. This is where Maven stores downloaded dependencies (JAR files, POM files, etc.) from remote repositories like Maven Central. These dependencies are cached locally to avoid repeatedly downloading the same artifacts, which can save time and bandwidth.

   - `.m2/repository/`: This is the location where all downloaded dependencies are stored in a structured directory hierarchy based on the Maven coordinates of the artifacts (group ID, artifact ID, version, etc.).

2. **Settings**: The `.m2` folder may also contain a `settings.xml` file, which allows you to configure Maven settings. This file can be used to specify custom repositories, proxy settings, and other configuration options.

   - `.m2/settings.xml`: The Maven settings file can be customized to suit your project's needs. You can create this file if it doesn't exist or modify an existing one.

3. **Wrapper (Optional)**: In some projects, you might find a `.m2/wrapper` directory. This is part of the Maven Wrapper mechanism, which allows you to include a version of Maven with your project. It ensures that everyone working on the project uses the same version of Maven, reducing compatibility issues.

   - `.m2/wrapper/`: This directory contains the Maven Wrapper files, such as `maven-wrapper.properties` and the `maven-wrapper.jar` file.

The `.m2` folder is important for managing and caching project dependencies when working with Maven. It helps ensure that your builds are reproducible and efficient by storing downloaded artifacts locally, reducing the need to fetch them from remote repositories repeatedly. It also provides a way to configure Maven's behavior through the `settings.xml` file.



.m2 folder is the default folder used by maven to store its:

    settings.xml file which specifies properties, like the central repository to download your dependencies, the location of the so-called localRepository
    by default, the localRepository in which maven stores all the dependencies your project might need to run.

Basically, when you build a Java application, the JDK only is not enough. You might need 3rd part libraries to help during the development. For instance:

    A lib to read CSV file
    A lib to do unit tests
    A lib to indicate weather ?

Anyway, without Maven, you'd be forced to download everything onto your computer, and indicate manually to your Java apps where to find those dependencies. That is the role of maven. It is a dependency management tool, that centralize in a single place the dependencies your project has, and give you in a standard way access to those librairies, in order to make you more efficient.

By default, maven fetches the dependencies from this website: https://repo1.maven.org/maven2/.

In term of efficiency, it is better to share the same localRepository across your projects, as it avoids maven from downloading the same dependencies again... I don't even know if there is a way, and if not, that is for a good reason: It is useless to have different local Repository in your computer


----------
------------

Q9 : what are the settings you need to do in pom.xml or any other settings you need to do before running mvn in deploy ?
- ans :

Before running the `mvn deploy` command to deploy your Maven project, there are several settings and configurations you need to ensure are correctly set up in your project's `pom.xml` and Maven settings. Deploying a project typically involves publishing artifacts (e.g., JAR files) to a remote repository (e.g., a company's internal repository or a public repository like Maven Central). Here are the key settings and configurations you should check:

**1. `<distributionManagement>` in pom.xml**: In your project's `pom.xml`, you should have a `<distributionManagement>` section that specifies the location where your project should be deployed. This includes the URL of the remote repository where the artifacts will be published and the repository ID used to reference it. For example:

```xml
<distributionManagement>
    <repository>
        <id>my-repo</id>
        <url>https://example.com/maven-repo/</url>
    </repository>
</distributionManagement>
```

**2. Authentication Credentials**: Ensure that you have the necessary authentication credentials (username and password) to access the remote repository specified in your `<distributionManagement>` settings. These credentials are usually configured in your Maven settings file (`~/.m2/settings.xml`) or provided through environment variables or other secure means.

   ```xml
   <servers>
       <server>
           <id>my-repo</id>
           <username>your-username</username>
           <password>your-password</password>
       </server>
   </servers>
   ```

**3. Plugin Configuration**: You may need to configure the `maven-deploy-plugin` in your `pom.xml` to specify which artifacts should be deployed and how. Here's an example configuration:

   ```xml
   <build>
       <plugins>
           <plugin>
               <groupId>org.apache.maven.plugins</groupId>
               <artifactId>maven-deploy-plugin</artifactId>
               <version>3.0.0-M1</version> <!-- Use the appropriate version -->
               <configuration>
                   <skip>true</skip> <!-- Set to false to enable the plugin -->
               </configuration>
           </plugin>
       </plugins>
   </build>
   ```

**4. Version and Packaging**: Ensure that your project's `<version>` and `<packaging>` elements are correctly set in the `pom.xml`. The `<version>` should be unique for each deployment, and `<packaging>` should specify the type of artifact (e.g., JAR, WAR, POM).

**5. GPG Signing (Optional)**: If you're deploying to a secure repository, you might need to sign your artifacts using GPG (GNU Privacy Guard). Maven provides plugins like `maven-gpg-plugin` for this purpose. You'll need to configure it in your `pom.xml` and set up GPG keys.

**6. Verify Dependencies**: Ensure that your project's dependencies and plugins are correctly defined in your `pom.xml`. Verify that they are accessible and available in the repositories you are deploying to.

**7. Clean Build**: Before deploying, it's a good practice to perform a clean build using `mvn clean install` to ensure that your project is built without any issues.

Once you've configured these settings in your `pom.xml` and Maven settings, you can run `mvn deploy` to deploy your project to the specified remote repository. Make sure you have the necessary permissions and access rights to publish to the remote repository.


Before running mvn deploy, you need to make sure that the following settings are configured in your pom.xml or in your Maven settings file (settings.xml):

    Repository information: You need to specify the repository where you want to deploy your artifacts. This can be done in the <distributionManagement> section of your pom.xml file:

<distributionManagement>
  <repository>
    <id>my-repository</id>
    <url>https://my-repository.com/releases</url>
  </repository>
</distributionManagement>

If you are deploying snapshot artifacts, you will also need to specify a snapshot repository:

<distributionManagement>
  <snapshotRepository>
    <id>my-snapshot-repository</id>
    <url>https://my-snapshot-repository.com/snapshots</url>
  </snapshotRepository>
</distributionManagement>

    Credentials: If the repository where you are deploying your artifacts requires authentication, you will need to configure your credentials in your Maven settings file (settings.xml). This can be done in the <servers> section:

<servers>
  <server>
    <id>my-repository</id>
    <username>my-username</username>
    <password>my-password</password>
  </server>
</servers>

If you are deploying to a private repository, you may also need to configure a proxy in your Maven settings file.

Once you have configured your repository information and credentials, you can deploy your artifacts by running the following command:

mvn deploy

This will deploy your artifacts to the repository that you specified in your pom.xml file.

In addition to the above settings, there are a few other things you may want to do before running mvn deploy:

    Make sure that your artifacts are built and packaged correctly. You can do this by running the mvn package command.
    Test your artifacts. It is a good idea to test your artifacts before deploying them to a production environment.
    Create a backup of your artifacts. This is in case something goes wrong with the deployment process.


    


-----------
------------


Q10 : have you build any maven projects in local ? if you to maven build first time it takes less time to build and next time it will takes less time to build, why it happens ?
- ans :
I haven't personally built Maven projects, but I can explain why the build time tends to decrease after the first build:

1. **Caching Dependencies**: During the first build of a Maven project, the build process resolves and downloads project dependencies (such as libraries and plugins) from remote repositories like Maven Central. These dependencies are typically cached in your local Maven repository (`~/.m2/repository`). When you build the project again, Maven checks the local repository first and uses the cached dependencies if they haven't changed. This significantly reduces the time required for dependency resolution and download.

2. **Incremental Builds**: Maven is designed to perform incremental builds. It means that it only recompiles and rebuilds parts of the project that have changed since the last build. If you haven't made substantial changes to your code or resources, Maven will reuse the previously compiled classes and other artifacts, further reducing build time.

3. **Plugin Optimization**: Maven plugins often employ various optimization techniques. For example, plugins like `maven-compiler-plugin` and `maven-surefire-plugin` can be configured to skip compilation and testing if nothing has changed, saving time during subsequent builds.

4. **Dependency Check**: Maven uses a checksum-based mechanism to check whether dependencies have changed. If the checksum of a dependency hasn't changed since the last build, Maven knows it doesn't need to re-download or rebuild that dependency, further speeding up the build process.

5. **Local Repository Cleanup**: Over time, your local repository may accumulate unused or outdated artifacts. Running `mvn clean install` or similar commands can help clean up the local repository, ensuring that only necessary artifacts are present. This can lead to faster builds because Maven won't waste time resolving and checking unnecessary dependencies.

6. **Parallel Builds**: Maven supports parallel builds using the `-T` (or `--threads`) option. This can significantly reduce build time by allowing multiple modules or projects to be built simultaneously.

7. **Use of Build Profiles**: Maven allows you to define different build profiles in your `pom.xml`. By selectively enabling or disabling certain profiles, you can tailor the build process to your needs, potentially saving time on unnecessary tasks.

In summary, Maven optimizes build times by caching dependencies, performing incremental builds, and employing various strategies to avoid unnecessary work during subsequent builds. This is particularly helpful for developers, as it reduces the time required for testing and development iterations.


Yes, I have built Maven projects in local. On the first build, Maven will:

   Download all dependencies from the remote repository to the local repository.
    Compile all source code.
    Run all tests.

On subsequent builds, Maven will only download dependencies that have changed, compile source code that has changed, and run tests that have changed. This is because Maven keeps track of the dependencies and source code that have changed since the last build.

There are a few reasons why Maven builds can take less time on the second and subsequent builds:

.

   Maven does not need to download dependencies that are already in the local repository.
    Maven can compile source code that has not changed in parallel, which can significantly speed up the build process.
    Maven can skip running tests that have not changed, which can save a lot of time if your project has a large number of tests.

In addition to these factors, there are a number of other things that can affect the speed of a Maven build, such as the size and complexity of your project, the number of dependencies, and the hardware that you are using.

Here are some tips for speeding up Maven builds:

   Use a local repository to store your dependencies. This will reduce the amount of time that Maven needs to spend downloading dependencies from the remote repository.
    Use a parallel build. This will allow Maven to compile source code in parallel, which can significantly speed up the build process.
    Use a build cache. This will allow Maven to skip compiling source code that has not changed since the last build.
    Optimize your tests. This can be done by writing smaller, more focused tests, and by using mocking and stubbing to avoid unnecessary external dependencies.
    Use a faster machine. If possible, use a machine with more CPU cores and more memory. This will allow Maven to run more tasks in parallel and to compile code more quickly.








-----
------

----------------------------

Q11 : how to get present working folder ? 
- ans :

In Bash scripting, you can obtain the present working folder (the current directory) using the `pwd` command, which stands for "print working directory." This command prints the absolute path of the current directory to the standard output.

Here's how you can assign the present working folder to a variable in a Bash script:

```bash
current_folder=$(pwd)
echo "Present working folder is: $current_folder"
```

This script will store the current directory in the `current_folder` variable and then print it.

If you want the name of the current directory (i.e., just the folder's name without the full path), you can use the `basename` command to extract it:

```bash
current_folder_name=$(basename $(pwd))
echo "Present working folder name is: $current_folder_name"
```

This script first uses `pwd` to get the absolute path of the current directory and then uses `basename` to extract only the folder's name.

thread : https://stackoverflow.com/questions/1371261/get-current-directory-or-folder-name-without-the-full-path


-----
-------

Q12 : how to copy files from local windows machine to cloud based linux machine , suppose i dont have any admin access ?
- ans :

If you don't have admin access to the Linux machine but have SSH access, you can use secure file transfer methods like SCP (Secure Copy Protocol) or SFTP (SSH File Transfer Protocol) to copy files from your local Windows machine to the cloud-based Linux machine. Here's how you can do it:

**Using SCP (Secure Copy Protocol):**

1. **Open a Command Prompt or PowerShell window** on your Windows machine.

2. **Use the `scp` command** to copy files from your local machine to the remote Linux machine. The basic syntax is as follows:

   ```bash
   scp [options] source_file_or_directory user@hostname:/path/to/destination
   ```

   - `[options]` are optional flags you can use, such as `-r` for recursive copy.
   - `source_file_or_directory` is the file or directory you want to copy from your local machine.
   - `user` is your username on the remote Linux machine.
   - `hostname` is the IP address or hostname of the remote Linux machine.
   - `:/path/to/destination` is the path on the remote machine where you want to copy the file(s).

   For example, to copy a file named `example.txt` from your local machine to the home directory of your user on the remote Linux machine, you can use:

   ```bash
   scp example.txt user@hostname:~/ 
   ```

   You will be prompted to enter your password for the remote machine.

**Using SFTP (SSH File Transfer Protocol):**

1. **Open an SFTP client** on your Windows machine. You can use dedicated SFTP clients like WinSCP or use built-in SFTP functionality in some SSH clients like PuTTY.

2. **Connect to the remote Linux machine** by entering the hostname or IP address, your username, and the SSH key or password.

3. **Use the SFTP client's interface** to navigate to the local directory containing the files you want to copy and the remote directory where you want to copy them.

4. **Drag and drop the files** from your local machine to the remote machine using the SFTP client's interface. The files will be transferred securely over SSH.

Remember that for both SCP and SFTP, you need to have SSH access to the remote Linux machine, and your user account on that machine should have appropriate permissions to write to the destination directory. If you encounter any issues related to file permissions or access, you may need to contact the system administrator or the owner of the remote machine for assistance.

--------
---------

Q13 : a shell script named test.sh can acept 4 parameters i.e a,b,c,d that parameters wont supplied in order always and number parameters might also vary ( only 2 parameters user might supply sometimes), how to identify position of letter c ?
- ans :

To identify the position of the letter "c" among the four parameters (`a`, `b`, `c`, and `d`) passed to your shell script `test.sh`, you can use a simple shell script that iterates through the arguments and checks each argument for the presence of the letter "c." Here's a basic example of how you can do this in a Bash script:

```bash
#!/bin/bash

# Initialize variables to store the positions of 'c' (assuming not found initially).
position_c1=""
position_c2=""
position_c3=""
position_c4=""

# Loop through the script's arguments.
for arg in "$@"; do
  case "$arg" in
    *c*)
      # Check if the argument contains 'c'.
      # Depending on the position of 'c', set the corresponding position variable.
      if [[ -z "$position_c1" ]]; then
        position_c1="$arg"
      elif [[ -z "$position_c2" ]]; then
        position_c2="$arg"
      elif [[ -z "$position_c3" ]]; then
        position_c3="$arg"
      else
        position_c4="$arg"
      fi
      ;;
  esac
done

# Output the positions of 'c'.
echo "Position of 'c' among the parameters:"
echo "1st position: $position_c1"
echo "2nd position: $position_c2"
echo "3rd position: $position_c3"
echo "4th position: $position_c4"
```

Save this script as `test.sh`, make it executable (`chmod +x test.sh`), and then you can run it with various arguments, such as:

```bash
./test.sh a b c d
./test.sh c d a
./test.sh b d
./test.sh c
```

The script will identify the positions of "c" among the parameters, and if "c" is not present in a parameter, the corresponding position variable will remain empty.

Keep in mind that this script assumes that you are passing a maximum of four parameters (`a`, `b`, `c`, and `d`). If you expect more parameters, you can extend the script accordingly.

OR


Another method to identify the position of the letter "c" among the parameters in your shell script is to iterate through the arguments using a `while` loop and maintain a counter for argument position. When "c" is found in an argument, you can store its position. Here's an example:

```bash
#!/bin/bash

# Initialize the counter.
position=1

# Iterate through the script's arguments.
while [ $# -gt 0 ]; do
  arg="$1"  # Get the first argument.

  # Check if the argument contains 'c'.
  if [[ "$arg" == *c* ]]; then
    echo "'c' found at position $position: $arg"
  fi

  # Move to the next argument and increment the position.
  shift
  ((position++))
done
```

Save this script as `test.sh`, make it executable (`chmod +x test.sh`), and then you can run it with various arguments, such as:

```bash
./test.sh a b c d
./test.sh c d a
./test.sh b d
./test.sh c
./test.sh e f g
```

This script will identify and print the positions of "c" among the parameters, and it can handle any number of parameters in any order.

--------------------------
-------------------------
-----------------------

Q11 : Have you worked on ansible adhoc command ?
- ans :

Q12 : why we need adhoc acnsible commands, give scenario where you have used ansibe adhoc command ?
- ans :

Q13 : when i need detailed logs on executing ansible-playbook what option i need to use , basically it gived a brief but i want detailed command ?
- ans :

Q14 : what is ansible.cfg file ?
- ans :

Q15 : what are the modules have you worked on ?
- ans :

Q16 : which module will you use for getting the file from node to master ?
- ans :

Q17 :  lets say i have playbook which has 5 tasks in playbook, first 2 tasks should run on local machine ( ansible master ) and other 3 tasks should run on node ?
- ans :



----------------------------------

Q18 :  How to save only last 5 builds of jenkins job? 
- ans :

Q19 :  Have you worked on Jenknsfile?
- ans :

Q20 : can we use docker container as a node in Jenkinsfile? 
- ans :

Q21 : Who will handle docker container creation and deletion ( docker container is jenkins worker node for just running a job ) ? 
- ans :

Q22 : If i am building a maven project always docker container is fresh instance it will try to download dependency from repository, what measures you will take to reduce build time?
- ans :


Q23 :  Why we need multi branch pipeline?
- ans :

Q24 :  If you forget Jenkins password, how would you login back?
- ans :


-------------------------------------

Q26 : Any best practices for docker ?
- ans :

Q27 : Difference between docker kill and docker stop ?
- ans :

Q28 : command to list containers which state is exited ?
- ans :

Q29 : command to cleamup docker host ( deleting stopped containers, dangling images and unused networks ) ?
- ans :

Q30 : What version of docker you have used ? , specific reason to use that perticular version ?
- ans :

Q31 : can we have multiple CMD in Dockerfile ?
- ans :

Q32 : Have you worked on docker swarm and docker compose ?
- ans :


-----------------------

Q33 : Can we have multiple conatiners in a pod?
- ans :

Q34 : Can we have similar conatiners in a pod? Lets say i have 4 conatiners, one of them has failed how would you check which container has failed?
- ans :

Q35 : What is liveness and readiness probe? Why we need them?
- ans :

Q36 : Have you worked on kubernetes monitoring? Which tools you have used?
- ans :

Q37 : Can we deploy a pod on particular node?
- ans :

-----------------------
















