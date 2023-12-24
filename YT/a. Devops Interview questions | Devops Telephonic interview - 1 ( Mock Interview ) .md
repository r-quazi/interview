
 ## Devops Interview questions | Devops Telephonic interview - 1 ( Mock Interview ) 
 
* Mock : https://www.youtube.com/watch?v=i7YJesoeWFI&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq
* Ans : https://www.youtube.com/watch?v=5w8qVukxXXY&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=9
 
---------

Q1 : Brief me all the tools you have worked on and daily activites you used to work on ?
- ans :
I started my carrier as Wordpress devloper in an NGO where i have devloped website and integrated razorpay payment method , added O Auth for facebook login and gmail login using the APIs and  worked with cloudflare as  CDN which helped to decrease  the latency also reduced some ddos attacks, integrated mailchimp for mass email and done some admin activities on cpanel.


later i joined HB initiatives as a devops engineer that was an startup here my responsibilities include creating ci cd pipeline , code quality check usning sonarqube , dockerizing the app, and used jfrog for the artifact after the testing phase i deployed to aws where i used s3, cloudfront, route53 , ecr. and  fargate.


i joined amazon as a cloud/client support associate later moved to build and release engineer and now supporting as resolution specialist. i won as bright thinker award 3 times for improving the process , reducing the waste, creating dashboard which improved the productivity .


we were launching a new crm software and that was the pilot project for india and germany region and both regions had around 35-40 microservices and we created seperate pipeline for these , for planning we have internal tools river, sim , tt , quip, quip kanban board etc and a wiki site for documentation .
The code was available on codecommit we used aws devops services like codebuild codecommit , codedeploy , cloud9, artifacts were stored in s3, codeguru , etc.


in CSA i worked with germany, austria, japan , na clients. they might come up with multiple queries and we check the accounts and help them with the solutions.  i worked for this role for few months only later i used to perform aws related tasks it can managing route52, elb , configuring lambda,aws transcribe, etc generally it depends on what task assigned to me.


few projects that i worked on are :

we had new hiring aroung 450 nhts in retail domain and they upload picture to the profile so whenever they upload it used to store in s3 so the issue was NHTs were uploading images of 2-3 MB which directly shooted the s3 cost , so we had configured an event whenever a upload detects in bucket it used to trigger a lambda fuction which reducec the cost and store the image in another bucket and we had added a lifecycle policy to the first s3 bucket. so 1st it take 20 mb to stores 10 images afetr that it used to take 4 MB and the cost was reduced.


i have worked with migrating the monolith architect to serverless as well, we  had nodeapp running on ec2 and databse were configured on that ec2 only though it was for internal team however sometimes we need to scale and we need to scale the whole ec2 which is not a good idea, we migrated the mysql server from ec2 to amazon aurora serverless with downtime of around 50 mins and backup restore took around 70 mins.  uploaded the website from ec2 to s3 which reduced the cost and no need to manager extra overhead of autoscaling, loadbalancing etc. 


one of the teams requirement was to deploy on lightsail that was a lamp architecture lightsail is quite easy as compared to ec2 however if we need more customization we should prefer ec2 only. the db creation is just a click away , can launch apache and php server in just a single click , lightsail also supports cdn and loadbalancer etc.

 few other configuration need for every project like cloudwatch, IAM, lifecycle policies, macie, tower and organization , vpc, security group etc.


whenever a project or task assigned to me i always go to quip that was the project manageement tool we have used we can also use jira and confluenec , so i aways update the details , find the related information and once resolved update the documentation there.

__________

# Git :

Q2 : so you worked on git right , so it only push , pull or you have also worked on admin activity ?
- ans :


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


```
both version control
 - Git : VCS
 - SVN : RCS

Git VS SVN : 
  - operates locally
  - can code without internet / connecting to main repo
  - need to connect to repo for push n pull
  - helps limit network traffic 
  - reduces cost ( AI LLMP repo 1.8 GB )
  -  SVN limited offline capabiloties
  - avoid single oint o failures , repo in every  vm
  - if deleted can restore  -- branches ALL
  - svn can be single point of fail ( untill backup )
  - in git dev canwork independently  merge conflicts can be resolved
  - svn better for RBAC , 

selection Git vs SVN depends on security
code commit no svn , we need to migrate svn to git to codecommit

azure support both dvcs and cvcs

```
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


```
use .gitignore
text file
can add folder or file name supports regex aswell
autogenerated with VScode , gitwebsite need to select type of project
templates available aswell
fole located in root directory of repo
git check-ignore -v filename
0r we can use cat ,gitinnore | grep filename


```
We can use the .gitignore file if we need some files which are not to be pushed to main repository.



we can add file or folder names in gitignore file, if we are using VS Code this file will be generated automatically and content of gitignnore depends on project we are creating. or

there are various templates are also available on the ietrnet

this file is located in the root firectory of the repo and it is a plain text file ans it supports the regex and pattern match

if our gitignore file is long or we are in some other folder we can use 'git check-ignore -v path/to/ignored/file to chewck if the file is in gitignore or not


--------
--------


Q5 : Difference between git pull and git fetch ?

- ans :

```
Fetch :
 - gives information of new changes from remote repo without merging
 - data stored in .git 
 - can review changes before merging
 - less merge conflicts

Pull : 
 - addition of git fetch and git merge
 -  merges the code
 - high chances of merge conflicts

fetch is safer version  and non destructive than pull 
```

Git fetch vs git pull

Git fetch gives the information of new changes from the remote repo without merging in thw current branch and the data is tored in .git we can revew the changes and git merge can be done and while using git fetc there are less chances of merge conflict because we are aware what previous changes has been done and depending on that git merge can be done

however

git pull is addition of git fetch and git merge git pull brings all the changes made to remote repo and merges in our current branch and our repository will be updated, In this case merge conflict may arise 1 there are changes at the same place.

we can say git fetch is the safe and non destructive of these 2 commands


---------
---------

Q6 : How to clone specific branch in  git ?

- ans :

```
git clone --single-branch --branch branch name branchurl

--single-branch : will clone master only
--branch : specific branch
--depth :  commit history , saves the bandwith

```
To clone a specific branch we can use -b flag, or we can also use ` git clone --single-branch --branch < branch name> <remote repo url> `

if we use only --single-branch by default it will clone master or main only and for specific branch we need to use --branch, we can use --depth to save the bandwith

there are other ways as well like cloning the repo with all branches and checkout to specific branch however that doesnt answer the question to clone specific branch only.

-----
-----

-------------------------

# Maven :

Q7 : When i issue mvn install what all things happen in background ?
- ans :

Maven is a build automation tool used primarily for the java projects . Whenever we issue mvn install command several things happen in the background , first it frdames a dependency tree on the pom.xml file and on  all the subprojects under super pom or the root pom however  it depdends on where we are running mvn install command generally we run where the super pom is located. then it sownloads , compiles all the needed components id directory .m2



1. **Parsing the Project**:  POM  XML file contains project metadata, dependencies, plugins, and build instructions. Maven checks to make sure that the POM file is well-formed and contains all of the required information.

2. **Dependency Resolution**: Maven checks the local repository (usually located at `~/.m2/repository`) to see if any of the project's dependencies are already present. If not, it proceeds to download them from remote repositories specified in the `pom.xml` (such as Maven Central or a corporate repository). Maven downloads all of the project's dependencies from the remote Maven repositories to the local Maven repository.

3. **Compiling Source Code**: Maven compiles the Java source code in your project, typically located in the `src/main/java` directory. It also compiles any test code located in the `src/test/java` directory. Maven compiles the project's Java source code into Java bytecode (bytecode is the machine code that is executed by the Java Virtual Machine).

4. **Running Tests**: If you have defined unit tests in your project (usually located in the `src/test/java` directory), Maven will execute these tests. If any tests fail, the build process will typically stop, and the project won't be installed. Maven runs the project's unit tests to ensure that the code is working as expected.

5. **Packaging**: Maven packages your project into a specific format, depending on the packaging type defined in the `pom.xml`. Common packaging types include JAR (Java Archive), WAR (Web Application Archive), and others. Maven packages the project's compiled bytecode and other resources into a JAR (Java Archive) file.

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



The following example shows how to use the mvn install command to install a multi-module Maven project:

mvn clean install -am

This command will clean the build artifacts for all of the project's modules, compile the source code for all of the modules, run the unit tests for all of the modules, package all of the modules, and install all of the modules' JAR files to the local Maven repository.

 

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

 The `.m2` folder is a directory that is `C:\Users\<username>` on Windows or `/Users/<username>` on macOS and Linux). This folder is created and used by Apache Maven, a popular build automation and project management tool  used for Java projects.

Here's what the `.m2` folder contains:

1. **Repository**: The most important subdirectory .  Maven stores downloaded dependencies (JAR files, POM files, etc.) from remote repositories like Maven Central. These dependencies are cached locally to avoid repeatedly downloading the same artifacts, which can save time and bandwidth.

 dependencies are stored in a structured directory hierarchy based on the Maven coordinates of the artifacts (group ID, artifact ID, version, etc.).

2. **Settings**: The `.m2` folder may also contain a `settings.xml` file, which allows you to configure Maven settings. This file can be used to specify custom repositories, proxy settings, and other configuration options.


3. **Wrapper (Optional)**:  This is part of the Maven Wrapper mechanism, which allows you to include a version of Maven with your project. It ensures that everyone working on the project uses the same version of Maven, reducing compatibility issues.

This directory contains the Maven Wrapper files, such as `maven-wrapper.properties` and the `maven-wrapper.jar` file.

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




If you are deploying snapshot artifacts, you will also need to specify a snapshot repository:
```
<distributionManagement>
  <snapshotRepository>
    <id>my-snapshot-repository</id>
    <url>https://my-snapshot-repository.com/snapshots</url>
  </snapshotRepository>
</distributionManagement>
```
Credentials: If the repository where you are deploying your artifacts requires authentication, you will need to configure your credentials in your Maven settings file (settings.xml). This can be done in the <servers> section:
```
<servers>
  <server>
    <id>my-repository</id>
    <username>my-username</username>
    <password>my-password</password>
  </server>
</servers>
```
If you are deploying to a private repository, you may also need to configure a proxy in your Maven settings file.

Once you have configured your repository information and credentials, you can deploy your artifacts by running the following command:

mvn deploy

This will deploy your artifacts to the repository that you specified in your pom.xml file.




-----------
------------


Q10 : have you build any maven projects in local ? if you to maven build first time it takes less time to build and next time it will takes less time to build, why it happens ?
- ans :

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

# Linux :


Q11 : how to get present working folder ? 
- ans :


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

 you can use secure file transfer methods like SCP (Secure Copy Protocol) or SFTP (SSH File Transfer Protocol) to copy files from your local Windows machine to the cloud-based Linux machine. Here's how you can do it:

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

or we can do using ansible , or uploading a file to stirage solution and downloading in vm via storage solution we have.

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
--------------------------
--------------------------

# ANSIBLE :


Q11 : Have you worked on ansible adhoc command ?
- ans :

Yes, I have worked on Ansible ad hoc commands. I have used them to perform a variety of tasks, including:

    Rebooting servers
    Copying files to multiple servers
    Managing packages on servers
    Creating and deleting users and groups on servers
    Checking the status of services on servers
    Gathering information about servers

I have also used Ansible ad hoc commands to automate more complex tasks, such as:

    Deploying a new application to multiple servers
    Configuring a load balancer
    Setting up a new VPN

I find Ansible ad hoc commands to be a very powerful and flexible tool for automating tasks on servers. They are easy to use and can be used to automate a wide variety of tasks.

Here are some examples of Ansible ad hoc commands that I have used:

    Reboot all servers in the "webservers" group:

ansible webservers -m reboot

    Copy the file /etc/hosts to all servers in the "all" group:

ansible all -m copy -a "src=/etc/hosts dest=/tmp/hosts"

    Install the nginx package on all servers in the "webservers" group:

ansible webservers -m package -a "name=nginx state=present"

    Create a new user named myuser on all servers in the "all" group:

ansible all -m user -a "name=myuser state=present"

    Check the status of the httpd service on all servers in the "webservers" group:

ansible webservers -m service -a "name=httpd state=started"

    Gather the IP addresses of all servers in the "all" group:

ansible all -m setup -a "filter={{ ansible_all_ipv4_addresses }}"

Ansible ad hoc commands can be used to automate a wide variety of tasks on servers. They are a powerful and flexible tool for system administrators and DevOps engineers.
Ansible ad-hoc commands are one-off commands that allow you to perform tasks on remote servers without creating and running Ansible playbooks. You can use ad-hoc commands for various tasks like checking server status, installing packages, copying files, and more.

Link : https://www.golinuxcloud.com/ansible-ad-hoc-commands/

------------


Q12 : why we need adhoc acnsible commands, give scenario where you have used ansibe adhoc command ?
- ans :

Ansible ad-hoc commands are useful in several scenarios where you need to perform quick, one-off tasks on remote servers without the overhead of creating and managing Ansible playbooks. Here are some common scenarios where ad-hoc commands come in handy:

1. **Quick Checks and Diagnostics:** Ad-hoc commands are great for quickly checking the status of remote servers. For instance, you can use the `ping` module to check if servers are reachable, or you can use the `command` module to run diagnostic commands like `df`, `free`, or `uptime` to gather system information.

   ```bash
   ansible all -m ping
   ansible all -m command -a "df -h"
   ```

2. **Package Management:** You can use ad-hoc commands to install or update packages on remote servers. For example, to install a package, you can use the `yum` or `apt` modules.

   ```bash
   ansible web_servers -m yum -a "name=httpd state=latest"  # Install the latest Apache HTTP Server
   ```

3. **File Operations:** Ad-hoc commands can be handy for copying files, creating directories, or managing files on remote servers.

   ```bash
   ansible app_servers -m copy -a "src=/path/to/local/file dest=/path/on/remote"
   ansible db_servers -m file -a "path=/path/to/directory state=directory"
   ```

4. **User and Permissions Management:** You can use ad-hoc commands to create users, change passwords, or adjust file permissions.

   ```bash
   ansible all -m user -a "name=johndoe password=<hashed_password>"
   ansible app_servers -m file -a "path=/var/www/html/owner=johndoe group=www-data mode=0644"
   ```

5. **Service Management:** You can start, stop, or restart services using ad-hoc commands. For example, to restart the Apache service:

   ```bash
   ansible web_servers -m service -a "name=httpd state=restarted"
   ```

6. **Gathering Information:** Ad-hoc commands can be used to gather information from remote servers, such as hardware details, network configurations, or software versions.

   ```bash
   ansible database_servers -m setup
   ```

7. **Emergency Fixes:** In urgent situations, when you need to apply a critical fix or patch across multiple servers quickly, ad-hoc commands can help you do that without having to create a playbook.

These are just a few examples of when Ansible ad-hoc commands can be valuable. They are particularly useful for tasks that don't need to be automated or when you need to perform tasks on a small set of servers in a hurry. However, for more complex and repeatable tasks, it's often better to use Ansible playbooks to maintain consistency and version control.


Ansible ad hoc commands are useful for a variety of tasks, including:

    Troubleshooting: Ad hoc commands can be used to quickly check the status of multiple servers or to run specific commands on a set of hosts. For example, you could use an ad hoc command to check if all of your web servers are running or to see if a particular process is responsive on each server.
    One-off tasks: Ad hoc commands can be used to perform one-time tasks, such as restarting a service, updating a configuration file, or deploying a new application. For example, you could use an ad hoc command to install a security patch on all of your servers or to update a configuration file on a group of web servers.
    Testing: Ad hoc commands can be used to test Ansible playbooks or to experiment with new Ansible modules. For example, you could use an ad hoc command to test a new playbook before deploying it to production or to see how a new module works on a specific server.

Example scenario:

I have used Ansible ad hoc commands to quickly troubleshoot a production issue. I was alerted that our website was down, and I needed to determine the root cause of the issue. I used an ad hoc command to check the status of all of our web servers. I discovered that one of the servers was unresponsive. I then used another ad hoc command to connect to the unresponsive server and check the system logs. I found that the server had crashed due to a hardware failure. I was able to quickly identify and resolve the issue without having to manually log in to each server and check the logs individually.

Another example scenario:

I used Ansible ad hoc commands to deploy a new security patch to all of our production servers. I first tested the patch in a staging environment using Ansible ad hoc commands. Once I was satisfied that the patch was working correctly, I used Ansible ad hoc commands to deploy the patch to all of our production servers. I was able to deploy the patch quickly and efficiently without having to manually log in to each server and install the patch individually.

Ansible ad hoc commands are a powerful tool that can be used to automate a variety of tasks. They are quick and easy to use, and they can be used to troubleshoot problems, perform one-off tasks, test playbooks, and deploy applications.



------------------

Q13 : when i need detailed logs on executing ansible-playbook what option i need to use , basically it gived a brief but i want detailed command ?
- ans :

To generate detailed logs when executing an Ansible playbook, you can use the `-v` or `--verbose` option. Increasing the verbosity level with each occurrence of this option provides more detailed output. There are four levels of verbosity available:

1. `-v`: This is the default level and provides a moderate amount of information.
2. `-vv`: Increases verbosity to show more detailed information.
3. `-vvv`: Even more verbose output, useful for debugging.
4. `-vvvv` or `-vvvvv`: Maximum verbosity, providing extensive details for troubleshooting.

Here's an example of how to use the `-vv` option when running an Ansible playbook:

```bash
ansible-playbook -vv your_playbook.yml
```

By using increased verbosity levels, you'll get more information about what Ansible is doing during playbook execution. This can be helpful for diagnosing issues or understanding the step-by-step process of the playbook run.

Keep in mind that higher verbosity levels can produce a significant amount of output, so it's usually best to use them only when you need detailed information for troubleshooting or debugging purposes.

If you are using Ansible Tower, you can also enable verbose logging for individual executions. To do this, go to the Execution tab for the execution you want to view logs for and click the Verbose checkbox.

Once you have enabled verbose logging, you can view the logs by clicking the Logs tab. The logs will be displayed in a text editor, and you can scroll through them to view the details of the playbook execution.


Ansible also has built-in support for logging. Add the following lines to your ansible configuration file:

[defaults] 
log_path=/path/to/logfile

Ansible will look in several places for the config file:

    ansible.cfg in the current directory where you ran ansible-playbook
    ~/.ansible.cfg
    /etc/ansible/ansible.cfg


-------------------

Q14 : what is ansible.cfg file ?
- ans :

The `ansible.cfg` file is a configuration file used to customize and configure various settings for the Ansible command-line tool and the Ansible automation framework as a whole. This file allows you to set preferences, default values, and behavior for Ansible, which can help streamline your workflow and maintain consistency across your Ansible projects.

Here are some key aspects of the `ansible.cfg` file:

1. **Location:** By default, Ansible looks for the `ansible.cfg` file in the current directory or in the `/etc/ansible/` directory. You can specify a different location for the configuration file using the `ANSIBLE_CONFIG` environment variable.

2. **Sections:** The `ansible.cfg` file is organized into sections, each of which contains configuration options related to a specific aspect of Ansible. Common sections include `[defaults]`, `[inventory]`, `[ssh_connection]`, and others.

3. **Options:** Within each section, you can set various configuration options, such as the default inventory file, connection settings, verbosity level, and more. Each option is specified as a key-value pair.

Here's an example of a simple `ansible.cfg` file:

```ini
[defaults]
inventory = /path/to/your/inventory
remote_user = your_username
ask_pass = yes

[ssh_connection]
ssh_args = -o ControlMaster=auto -o ControlPersist=60s
```

In this example:

- The `[defaults]` section sets the default inventory file, the remote user to use when connecting to hosts, and specifies to prompt for the SSH password (`ask_pass`).
- The `[ssh_connection]` section configures SSH connection parameters, such as enabling SSH control master and specifying a control persist time.

You can create and customize the `ansible.cfg` file to meet your specific requirements. It's especially useful when you want to avoid specifying the same options repeatedly on the command line, making your Ansible commands more concise and maintainable. Additionally, you can create project-specific `ansible.cfg` files in your Ansible project directories to override or extend the global configuration.

Ansible provides several configuration files that you can use to customize its behavior. Here are three commonly used Ansible configuration files:

1. **ansible.cfg:** This is the main Ansible configuration file, and it allows you to set global configuration options that apply to all Ansible commands. You can have a global `ansible.cfg` file located in `/etc/ansible/` or a user-specific `ansible.cfg` file in your home directory (`~/.ansible.cfg`). This file typically includes options such as the default inventory file, remote user, verbosity level, and more.

2. **hosts (inventory) file:** While not a traditional configuration file, the Ansible hosts file (sometimes referred to as the inventory file) is crucial for specifying the hosts and groups that Ansible can manage. By default, this file is named `hosts` and is often located in the `/etc/ansible/` directory. However, you can specify a different inventory file using the `-i` option when running Ansible commands. The inventory file defines the target hosts, their IP addresses, connection details, and group memberships.

3. **ansible.cfg (project-specific):** In addition to the global and user-specific `ansible.cfg` files, you can create project-specific `ansible.cfg` files in your Ansible project directories. These project-specific configuration files override or extend the global configuration options. When you run an Ansible command within a project directory, Ansible will prioritize the settings from the project-specific `ansible.cfg` file if it exists. This allows you to tailor the configuration for each project while keeping a global configuration for Ansible.

Here's an example of how these configuration files work together:

- If you have a global `ansible.cfg` file in `/etc/ansible/` with certain settings.
- You can also have a user-specific `ansible.cfg` file in your home directory (`~/.ansible.cfg`) with different settings.
- When you run an Ansible command, Ansible will first check for a project-specific `ansible.cfg` file in the current directory. If it exists, Ansible will prioritize the settings in that file.
- If there's no project-specific `ansible.cfg` file, Ansible will use the settings from the user-specific `ansible.cfg` file.
- If no user-specific `ansible.cfg` file is found, Ansible will fall back to the global `ansible.cfg` file in `/etc/ansible/`.

This configuration hierarchy allows you to customize Ansible behavior at various levels, from global defaults to per-project settings.

The ansible.cfg file is a configuration file for Ansible, a popular open-source automation tool. It allows you to override the default settings for Ansible, such as the inventory file to use, the connection method, and the logging level.

The ansible.cfg file is searched for in the following order:

    The environment variable ANSIBLE_CONFIG
    The current working directory
    The user's home directory
    The /etc/ansible/ansible.cfg file

The first file found is used, and subsequent files are ignored.

Here are some examples of settings that you can configure in the ansible.cfg file:

    inventory: The path to the inventory file.
    remote_user: The username to use to connect to remote hosts.
    forks: The number of parallel processes to use when running playbooks.
    sudo_user: The user to use when running sudo commands on remote hosts.
    transport: The connection method to use, such as ssh or paramiko.
    gathering: Whether or not to gather facts about remote hosts before running tasks.
    roles_path: A list of paths to search for roles in.
    log_path: The path to the Ansible log file.

You can also use the ansible.cfg file to define custom variables and connection plugins.

Here is an example of a simple ansible.cfg file:

[defaults]
inventory = $HOME/.ansible/hosts
remote_user = root
forks = 150
sudo_user = root
transport = smart
gathering = smart
roles_path = $HOME/.ansible/roles
log_path = /var/log/ansible.log

This file overrides the default values for the inventory, remote_user, forks, sudo_user, transport, gathering, and roles_path settings.

-----------



Q15 : what are the modules have you worked on ?
- ans :


I'm familiar with a wide range of Ansible modules and can provide information and examples for many of them. Ansible modules are pre-built, reusable components that allow you to perform specific tasks or operations on remote hosts. Here are some common Ansible modules:

1. **Command Modules:** These modules allow you to run commands on remote hosts. Examples include `command`, `shell`, and `raw`.

2. **File Modules:** File modules help with tasks related to managing files and directories. Examples include `copy`, `file`, `template`, and `lineinfile`.

3. **Package Modules:** Package modules are used for package management. Examples include `apt`, `yum`, and `dnf`.

4. **Service Modules:** Service modules help control system services. Examples include `service` and `systemd`.

5. **User Modules:** User modules allow you to manage user accounts and groups on remote hosts. Examples include `user` and `group`.

6. **Inventory Modules:** Inventory modules are used to gather information about your Ansible inventory. Examples include `ec2`, `azure_rm`, and `gcp_compute`.

7. **Database Modules:** Database modules enable interaction with databases. Examples include `mysql_db`, `postgresql_db`, and `mongodb_user`.

8. **Cloud Modules:** Cloud modules are used to manage cloud resources and instances. Examples include `aws_ec2`, `azure_rm_virtualmachine`, and `gcp_compute_instance`.

9. **Networking Modules:** Networking modules are designed for network device automation. Examples include `ios_command`, `nxos_command`, and `ios_facts`.

10. **System Modules:** System modules help with system-level tasks. Examples include `ping`, `reboot`, and `hostname`.

11. **Notification Modules:** Notification modules allow you to send messages or alerts. Examples include `mail`, `slack`, and `hipchat`.

12. **Utility Modules:** Utility modules provide various helper functions. Examples include `assert`, `debug`, and `wait_for`.

These are just a few examples of Ansible modules, and there are many more available for different use cases and technologies. If you have a specific module or task you'd like to know more about or if you have a question about how to use a particular module, please feel free to ask, and I'll provide more information and examples.

I have been trained on a massive dataset of text and code, including the Ansible documentation and source code. This means that I have a good understanding of how Ansible modules work and how to use them. I have also been trained on a variety of real-world Ansible playbooks and roles, which has given me experience with a wide range of Ansible modules.

Here are some specific Ansible modules that I have worked on:

    File modules, such as file and copy.
    Package modules, such as apt and yum.
    Service modules, such as service and systemd.
    User modules, such as user and group.
    Networking modules, such as ifconfig and route.
    Monitoring modules, such as ping and uptime.
    Cloud modules, such as aws and azure.

I can use these modules to perform a variety of tasks, such as:

    Install, upgrade, and remove software packages.
    Start, stop, and restart services.
    Create and manage users and groups.
    Configure network interfaces and routing tables.
    Monitor the health and performance of remote systems.
    Manage cloud resources, such as EC2 instances and Azure virtual machines.

I am still under development, but I am learning new Ansible modules all the time. I am also learning how to use Ansible modules in more complex and sophisticated ways.


Link : https://faun.pub/ansible-30-most-important-modules-for-devops-professional-part-1-fdd536b0790d


------------------


Q16 : which module will you use for getting the file from node to master ?
- ans :

To copy a file from a remote node (target host) to the Ansible control machine (master), you can use the `fetch` module. The `fetch` module is specifically designed for retrieving files from remote hosts. Here's an example of how to use it:

```bash
ansible <target_hosts> -m fetch -a "src=/path/on/remote dest=/local/destination flat=yes"
```

Explanation of the parameters:

- `<target_hosts>`: Specifies the host or hosts from which you want to fetch the file.
- `-m fetch`: Indicates that you want to use the `fetch` module.
- `-a`: Specifies the module arguments, including the source (`src`) and destination (`dest`) paths.
- `src`: The path to the file on the remote host that you want to fetch.
- `dest`: The local directory where you want to save the fetched file.
- `flat=yes`: This option tells Ansible to flatten the directory structure when copying, placing the fetched file directly in the destination directory without creating any subdirectories.

For example, to fetch a file named `example.txt` from a remote host with the IP address `192.168.1.100` and store it in the local `/tmp` directory, you can use the following command:

```bash
ansible 192.168.1.100 -m fetch -a "src=/path/to/remote/example.txt dest=/tmp flat=yes"
```

After running this command, the `example.txt` file from the remote host will be copied to the `/tmp` directory on your Ansible control machine.


The Ansible module to use for getting a file from a node to the master is the fetch module. This module works like the copy module, but in reverse. It is used for fetching files from remote machines and storing them locally in a file tree, organized by hostname. Files that already exist at the destination will be overwritten if they are different than the source.

To use the fetch module, you will need to specify the source file on the remote node and the destination directory on the master. You can also use the dest parameter to specify a specific filename for the destination file.

For example, the following playbook will fetch the file /etc/hosts from all remote nodes and store it in the /tmp/hosts directory on the master:

---
- hosts: all
  tasks:
    - name: Fetch /etc/hosts from remote nodes
      fetch:
        src: /etc/hosts
        dest: /tmp/hosts

If you want to fetch the file to a different directory, you can use the dest parameter. For example, the following playbook will fetch the file /etc/hosts from all remote nodes and store it in the /mnt/ansible/hosts directory on the master:

---
- hosts: all
  tasks:
    - name: Fetch /etc/hosts to /mnt/ansible/hosts
      fetch:
        src: /etc/hosts
        dest: /mnt/ansible/hosts

You can also use the fetch module to fetch multiple files from a remote node. To do this, you can use the src parameter to specify a list of files. For example, the following playbook will fetch the files /etc/hosts and /etc/hostname from all remote nodes and store them in the /tmp/ansible directory on the master:

---
- hosts: all
  tasks:
    - name: Fetch /etc/hosts and /etc/hostname from remote nodes
      fetch:
        src:
          - /etc/hosts
          - /etc/hostname
        dest: /tmp/ansible

The fetch module is a powerful tool for getting files from remote nodes to the master. It is easy to use and can be used to fetch a single file or multiple files from multiple nodes.


------------------


Q17 :  lets say i have playbook which has 5 tasks in playbook, first 2 tasks should run on local machine ( ansible master ) and other 3 tasks should run on node ?
- ans :

There are a few ways to run the first two tasks in your playbook on the local machine (Ansible master) and the other three tasks on the node:

    Use the local_action clause. The local_action clause allows you to run a task on the Ansible controller instead of on the managed node. To use the local_action clause, add it to the task you want to run on the local machine. For example:

- hosts: all
  tasks:
    - name: Install Python 3
      local_action:
        module: package
        name: python3
        state: present
    - name: Install Ansible
      local_action:
        module: package
        name: ansible
        state: present
    - name: Update all packages
      ansible.builtin.apt:
        name: "*"
        state: latest

    Use the delegate_to keyword. The delegate_to keyword allows you to run a task on a specific host instead of on all of the managed nodes. To use the delegate_to keyword, add it to the task you want to run on the node. For example:

- hosts: all
  tasks:
    - name: Update all packages
      ansible.builtin.apt:
        name: "*"
        state: latest
    - name: Start Apache
      delegate_to: node1
      ansible.builtin.service:
        name: apache2
        state: started
    - name: Start MySQL
      delegate_to: node2
      ansible.builtin.service:
        name: mysql
        state: started

    Use the -l or --limit option when running the playbook. The -l or --limit option allows you to specify which hosts to run the playbook on. To run the first two tasks in your playbook on the local machine, you would use the following command:

ansible-playbook -l localhost playbook.yml

To run the other three tasks in your playbook on the node, you would use the following command:

ansible-playbook -l node1,node2 playbook.yml

Which method you choose will depend on your specific needs and preferences. If you only need to run a few tasks on the local machine, then using the local_action clause is the simplest option. If you need to run more tasks on the local machine, or if you need to run the tasks on a specific host, then using the delegate_to keyword or the -l or --limit option is a better option.

Note: It is important to note that some tasks cannot be delegated to the local machine. These tasks include the include, add_host, and debug tasks.

You can achieve this by combining local actions and remote actions within a single Ansible playbook. Ansible allows you to specify tasks that should run locally on the control machine (Ansible master) and tasks that should run on the remote nodes.

Here's an example playbook structure with five tasks, where the first two tasks run locally on the control machine (Ansible master), and the remaining three tasks run on the remote nodes:

```yaml
---
- name: Example Playbook
  hosts: localhost  # This limits the playbook to run only on the Ansible control machine
  gather_facts: no  # Disable facts gathering for the local tasks

  tasks:
    - name: Task 1 (Local)
      debug:
        msg: "This task runs locally on the control machine."

    - name: Task 2 (Local)
      command: echo "This is a local command."
      register: local_result

- name: Example Playbook (Remote)
  hosts: your_target_group  # Define the group or host pattern for remote nodes
  gather_facts: yes  # Enable facts gathering for the remote tasks

  tasks:
    - name: Task 3 (Remote)
      debug:
        msg: "This task runs on the remote nodes."

    - name: Task 4 (Remote)
      # Add your remote task here

    - name: Task 5 (Remote)
      # Add another remote task here
```

In this playbook:

- The first two tasks (Task 1 and Task 2) are specified under the first play (`Example Playbook`) and are set to run on `localhost`, which means they run locally on the Ansible control machine.

- The remaining three tasks (Task 3, Task 4, and Task 5) are specified under the second play (`Example Playbook (Remote)`) and are set to run on your target group or hosts. Replace `your_target_group` with the appropriate group or host pattern that represents the remote nodes where you want to execute these tasks.

By structuring your playbook in this way, you can separate local and remote tasks while using the same playbook. This approach allows you to perform tasks on the Ansible control machine and remote nodes in a single playbook run.

Link : https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_strategies.html

--------
-----------------------
-----------------------
--------------------------



Q18 :  How to save only last 5 builds of jenkins job? 
- ans :
In Jenkins, you can configure build retention policies to keep only the last 5 builds of a job and automatically discard older builds. This helps to manage disk space and maintain a clean build history. To achieve this, you can use the "Log Rotation" feature in Jenkins. Here's how you can do it:

1. **Open the Jenkins Job Configuration:**

   - Navigate to the Jenkins dashboard.
   - Click on the job you want to configure (the job for which you want to retain only the last 5 builds).

2. **Configure Log Rotation:**

   - Scroll down to the "Build Discarder" section in the job configuration.
   - Select the "Log Rotation" option.

3. **Specify Build Retention Settings:**

   - In the "Log Rotation Strategy" dropdown, select "Builds to keep with artifacts."
   - In the "Days to keep artifacts" field, you can set the number of days you want to keep build artifacts. To retain only the last 5 builds, you can set this value to a relatively small number (e.g., 5).

   ![Jenkins Log Rotation](/images/jenkins-log-rotation.png)

4. **Save the Configuration:**

   - Scroll down to the bottom of the job configuration page.
   - Click the "Save" button to apply the changes.

Now, Jenkins will automatically retain only the last 5 builds of the job, and older builds will be deleted based on the retention settings you specified. This helps in managing disk space and ensures that only the most recent build history is preserved.

Keep in mind that the exact steps and options may vary slightly depending on the version of Jenkins you are using, but the general approach for configuring build retention remains consistent.

There are two ways to save only the last 5 builds of a Jenkins job:

1. Using the Jenkins UI

    Go to the Job Configuration page for the job.
    Scroll down to the Discard Old Builds section and check the box next to Discard old builds.
    In the Max # of builds to keep field, enter 5.
    Click Save.

The next time the job is run, Jenkins will automatically delete all builds older than the last 5.

2. Using the Jenkins CLI

    Open a terminal window and navigate to the Jenkins home directory.
    Run the following command:

jenkins job <job-name> config

This will open the job configuration in a text editor.

    Add the following lines to the configuration file:

<buildDiscarder>
  <logRotator numToKeepStr="5" artifactNumToKeepStr="5"/>
</buildDiscarder>

    Save the file and exit the text editor.

    Restart Jenkins.

The next time the job is run, Jenkins will automatically delete all builds older than the last 5.

Note: If you are using a Declarative pipeline, you can also configure Jenkins to keep only the last 5 builds by adding the following code to your pipeline script:

pipeline {
  options {
    buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
  }
  ...
}

Additional Considerations

    When configuring Jenkins to keep only the last 5 builds, it is important to keep in mind that you may need to retain older builds for compliance or auditing purposes.
    If you are unsure how many builds you need to keep, it is best to consult with your team or other stakeholders.
    You can also use the Build History Manager plugin to configure more granular build retention policies.


    
---------------------------------


Q19 :  Have you worked on Jenknsfile?
- ans :
Yes, I'm familiar with Jenkinsfiles. A Jenkinsfile is a text file that contains the definition of a Jenkins Pipeline. Jenkins Pipelines are a powerful way to define and automate your CI/CD (Continuous Integration/Continuous Deployment) processes. With Jenkinsfiles, you can describe your entire build and deployment process as code, which allows for versioning, code review, and repeatability.

Here are some key points about Jenkinsfiles:

1. **Declarative and Scripted Syntax:** Jenkins Pipelines can be defined using either Declarative or Scripted syntax. Declarative syntax provides a more structured and concise way to define pipelines, while Scripted syntax allows for more flexibility and customization using Groovy scripting.

2. **Version Control:** Jenkinsfiles are typically stored alongside your application code in a version control system (e.g., Git). This makes it easy to track changes to your CI/CD process and collaborate with team members.

3. **Pipeline Stages:** Jenkins Pipelines are divided into stages, each representing a step in your CI/CD process. Stages can include building, testing, packaging, deploying, and more.

4. **Parallel Execution:** Pipelines can execute multiple stages in parallel, which is useful for speeding up the build and deployment process.

5. **Error Handling:** Jenkinsfiles allow you to define error handling and recovery strategies. You can specify what to do if a stage fails, such as sending notifications or rolling back deployments.

6. **Integration with Tools:** Jenkins Pipelines can integrate with a wide range of tools and services, such as Docker, Kubernetes, AWS, and more, to orchestrate complex CI/CD workflows.

7. **Pipeline as Code:** The concept of "Pipeline as Code" means that your CI/CD process is defined, versioned, and managed just like your application code, promoting consistency and repeatability.

If you have specific questions about Jenkinsfiles, how to define them, or how to use them in your CI/CD process, please feel free to ask, and I'll be happy to provide more information or examples.

Yes, I have worked on Jenkinsfiles. I have helped users to write Jenkinsfiles for their projects, and I have also written Jenkinsfiles for my own projects.

Jenkinsfiles are a great way to automate the continuous integration and continuous delivery (CI/CD) process. They allow you to define the steps that need to be taken to build, test, and deploy your application in a single file. This can make your CI/CD process more efficient and reliable.

I am able to write Jenkinsfiles in both declarative and scripted syntax. Declarative syntax is the newer and more recommended syntax, as it is easier to read and write. However, scripted syntax can be used for more complex tasks.

Here is a simple example of a Jenkinsfile in declarative syntax:

pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building the application...'
        sh 'mvn clean package'
      }
    }
    stage('Test') {
      steps {
        echo 'Running the tests...'
        sh 'mvn test'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying the application...'
        sh 'scp target/my-app.jar user@example.com:/path/to/deploy'
      }
    }
  }
}

This Jenkinsfile defines a three-stage pipeline: build, test, and deploy. Each stage contains a list of steps that will be executed. For example, the build stage will build the application using Maven. The test stage will run the application's tests. And the deploy stage will deploy the application to a production server.

Jenkinsfiles can be used to automate a wide variety of tasks, including:

    Building and testing applications
    Deploying applications
    Running code reviews
    Sending notifications
    And much more

If you are using Jenkins to automate your CI/CD process, I recommend using Jenkinsfiles. They are a powerful tool that can help you to make your CI/CD process more efficient and reliable.


------------------


Q20 : can we use docker container as a node in Jenkinsfile? 
- ans :
Yes, you can use Docker containers as build agents (nodes) in a Jenkinsfile. This approach is often referred to as "Docker in Docker" (DinD) or "Container in Container" (CinC) and is a common practice in Jenkins Pipelines when you want to isolate build environments and run build steps inside Docker containers.

Here's a high-level overview of how you can use Docker containers as build agents in a Jenkinsfile:

1. **Define a Custom Docker Image:**
   - Create a custom Docker image that includes the necessary build tools, dependencies, and agents.
   - This image should have Jenkins agent software installed (usually using a JNLP agent) to allow Jenkins to communicate with it.

2. **Configure Jenkins:**
   - In your Jenkins configuration, ensure that Jenkins can access and use Docker. You may need to install and configure Docker on the Jenkins server.

3. **Create a Jenkins Pipeline:**
   - In your Jenkinsfile, define a pipeline that specifies the custom Docker image to be used as the build agent for specific stages or steps.

Here's a simplified example of a Jenkinsfile that uses a custom Docker image as a build agent:

```groovy
pipeline {
    agent {
        docker {
            image 'your-custom-docker-image:tag'
            args '-v /var/run/docker.sock:/var/run/docker.sock'  // Allows running Docker commands within the container
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo "Building inside Docker container"'
                // Add build steps specific to your project
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Testing inside Docker container"'
                // Add test steps specific to your project
            }
        }
        // Add more stages as needed
    }
}
```

In this example:

- The `agent` block specifies the use of a Docker container as the build agent.
- The `docker` block defines the custom Docker image to use. You should replace `'your-custom-docker-image:tag'` with the actual image name and tag you've created.
- The `args` option mounts the Docker socket from the host to the container, allowing Docker commands to be run within the container.

Inside the pipeline stages, you can run build and test steps specific to your project, all within the Docker container defined by the custom image.

This approach provides a high degree of isolation for your build environment, making it easier to manage dependencies and ensuring consistency across different builds. However, it's essential to properly secure and manage access to the Docker socket to prevent security risks.


Yes, we can use a Docker container as a node in a Jenkinsfile. This is useful for running builds and tests in a controlled environment, as well as for using specialized tools that are not available on the Jenkins master or slave nodes.

To use a Docker container as a node in a Jenkinsfile, we use the node step with the docker agent type. We can then specify the Docker image to use, as well as any additional parameters, such as the volume mounts and environment variables.

For example, the following Jenkinsfile will run a build and test stage in a Docker container based on the maven:latest image:

pipeline {
  agent any
  stages {
    stage('Build') {
      node {
        docker.image('maven:latest')
        sh 'mvn clean install'
      }
    }
    stage('Test') {
      node {
        docker.image('maven:latest')
        sh 'mvn test'
      }
    }
  }
}

We can also use a Docker container as a node in a Jenkins pipeline to run a specific command or script. For example, the following Jenkinsfile will run a shell script in a Docker container based on the ubuntu:latest image:

pipeline {
  agent any
  stages {
    stage('Run script') {
      node {
        docker.image('ubuntu:latest')
        sh './my-script.sh'
      }
    }
  }
}

Using Docker containers as nodes in a Jenkinsfile can provide a number of benefits, including:

    Isolation: Each Docker container runs in its own isolated environment, which can help to prevent conflicts between different builds and tests.
    Reproducibility: Docker containers are immutable, which means that the same environment can be used for each build and test, ensuring reproducible results.
    Scalability: Docker containers can be easily scaled up or down to meet the needs of the Jenkins pipeline.

Overall, using Docker containers as nodes in a Jenkinsfile is a great way to improve the efficiency, reliability, and scalability of your CI/CD pipeline.


------------------------------


Q21 : Who will handle docker container creation and deletion ( docker container is jenkins worker node for just running a job ) ? 
- ans :
In a Jenkins setup where Docker containers are used as worker nodes for running jobs (commonly referred to as Docker-based Jenkins agents), the responsibility for creating and deleting these Docker containers is typically managed by Jenkins itself. Jenkins dynamically creates and destroys these containers as needed to execute pipeline jobs or individual build steps.

Here's how it generally works:

1. **Job Execution Request:** When a Jenkins job is triggered (either manually or by a webhook or other automated means), Jenkins determines which agent or node should execute the job. If the job is configured to use a Docker-based agent, Jenkins proceeds with container creation.

2. **Container Creation:** Jenkins uses the Docker API to create a new container based on the specified Docker image. This container is isolated and typically contains the necessary tools and dependencies for the job.

3. **Job Execution:** Jenkins then schedules the job or build steps to run inside the newly created Docker container. The container acts as the build environment, and all the job's commands and scripts are executed within this container.

4. **Job Completion:** Once the job is completed, the container's state is saved and can be examined for logs, artifacts, or other outputs.

5. **Container Deletion:** After the job finishes and its output is collected, Jenkins automatically removes the Docker container. This cleanup process ensures that resources are efficiently managed, and containers don't accumulate unnecessarily.

Jenkins manages this entire process transparently to users, abstracting away the container creation and deletion details. The specific steps and configurations can vary based on your Jenkins setup, but Jenkins' built-in Docker Pipeline Plugin and Docker Swarm or Kubernetes integrations can help simplify the management of Docker-based agents.

It's important to note that this setup can provide excellent isolation between different build jobs and promotes reproducibility since each job runs in a fresh container. However, it's essential to properly configure and secure your Jenkins environment, especially if you're using Docker for build agents, to ensure security and resource management.

There are two main ways to handle Docker container creation and deletion for a Jenkins worker node that is only used to run a job:

1. Jenkins

Jenkins can be configured to create and delete Docker containers automatically. This can be done using the Docker Pipeline plugin.

To configure Jenkins to create and delete Docker containers automatically:

    Install the Docker Pipeline plugin.
    Create a new Jenkins pipeline.
    Add a Docker Compose stage to the pipeline.
    In the Docker Compose stage, specify the Docker image that you want to use for the worker node.
    Add a Post-build Actions section to the pipeline.
    In the Post-build Actions section, select the Delete Docker container option.

2. Kubernetes

If you are using Kubernetes to manage your Jenkins cluster, you can use the Jenkins Kubernetes Agent plugin to create and delete Docker containers automatically.

To configure Jenkins to create and delete Docker containers using Kubernetes:

    Install the Jenkins Kubernetes Agent plugin.
    Create a new Jenkins pipeline.
    Add a Kubernetes stage to the pipeline.
    In the Kubernetes stage, specify the Kubernetes pod template that you want to use for the worker node.
    Add a Post-build Actions section to the pipeline.
    In the Post-build Actions section, select the Delete Kubernetes pod option.

Which method to choose?

The best method to choose for creating and deleting Docker containers for Jenkins worker nodes depends on your specific needs. If you are only running a few jobs, then you may want to use the Jenkins method. However, if you are running a large number of jobs, or if you need to use Kubernetes to manage your Jenkins cluster, then you may want to use the Kubernetes method.

Additional considerations

Here are some additional considerations to keep in mind when creating and deleting Docker containers for Jenkins worker nodes:

    If you are using the Jenkins method, then you need to make sure that the Jenkins master has access to the Docker daemon.
    If you are using the Kubernetes method, then you need to make sure that the Jenkins master has access to the Kubernetes API server.
    You may want to consider using a tool such as Docker Swarm or Kubernetes to manage your Docker containers. This can help you to scale your Jenkins cluster and to make it more resilient.
    You may also want to consider using a tool such as Jenkins X to automate the creation and deployment of your Jenkins pipelines.

I hope this information is helpful. Please let me know if you have any other questions.

Link : https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjqsKri0ryBAxXQbmwGHUFyC4MQFnoECBoQAQ&url=https%3A%2F%2Fblog.thecloudside.com%2Fdocker-in-docker-with-jenkins-pod-on-kubernetes-f2b9877936f2&usg=AOvVaw0wV8d3gxvdwi6YIwYgYK0d&opi=89978449

-----------------

Q22 : If i am building a maven project always docker container is fresh instance it will try to download dependency from repository, what measures you will take to reduce build time?
- ans :
To reduce build time for a Maven project within a Docker container, you can take several measures to optimize the build process and minimize the need to download dependencies from the Maven Central Repository or other remote repositories during each build. Here are some strategies you can implement:

1. **Local Repository Caching:**
   - Configure your Docker image to have a local Maven repository cache. Maven stores downloaded dependencies in a local repository by default. By using a Docker image that already contains a pre-populated local repository, you can significantly reduce the need to download dependencies during each build.
   - Example Dockerfile snippet:

   ```Dockerfile
   COPY .m2 /root/.m2
   ```

   In this example, you copy your local `.m2` directory (containing the Maven repository cache) to the Docker image's `/root/.m2` directory.

2. **Multi-Stage Docker Builds:**
   - Use multi-stage Docker builds to create a temporary build image that downloads dependencies and builds your project. Then, copy the built artifacts (e.g., JAR files) to a smaller runtime image.
   - This approach ensures that the expensive dependency resolution and compilation steps are done once in the build image and do not need to be repeated in the runtime image.
   - Example multi-stage Dockerfile:

   ```Dockerfile
   # Build stage
   FROM maven:3.8.4 AS builder
   WORKDIR /app
   COPY pom.xml .
   RUN mvn dependency:go-offline
   COPY src src
   RUN mvn package

   # Runtime stage
   FROM openjdk:11
   COPY --from=builder /app/target/my-app.jar /app/
   WORKDIR /app
   CMD ["java", "-jar", "my-app.jar"]
   ```

3. **Maven Wrapper:**
   - Use the Maven Wrapper (a script and properties file bundled with your project) to ensure that the correct Maven version is used, even if the Docker image doesn't have Maven installed.
   - The Maven Wrapper downloads the specified Maven version automatically, reducing the need to install or configure Maven within the Docker image.
   - To generate a Maven Wrapper, you can run `mvn wrapper:wrapper` in your project.

4. **Docker Layer Caching:**
   - Leverage Docker's layer caching mechanism. Ensure that frequently changing files and dependencies are copied into the Docker image as late as possible in your Dockerfile.
   - Avoid invalidating the cache unnecessarily by changing files that don't affect the dependency resolution step.

5. **Docker BuildKit:**
   - Consider using Docker BuildKit, which provides more efficient layer caching and improved performance during Docker image builds.

6. **Artifact Repositories:**
   - If your organization permits, set up an internal Maven repository (e.g., Nexus or Artifactory) to cache dependencies. This can significantly reduce dependency download times.

By implementing these measures, you can optimize your Dockerized Maven build process and minimize build times, especially for projects with large or frequently changing dependencies.

If you are building a Maven project in a fresh Docker container every time, and the container is trying to download dependencies from the repository, this can significantly increase build time. There are a few measures you can take to reduce build time in this situation:

    Use a cached image. Instead of building a fresh image from scratch each time, you can use a cached image that already contains the Maven dependencies. This will save the time of downloading and installing the dependencies. To do this, you can use the --cache-from flag when running the docker build command. For example:

docker build --cache-from mvn-dependencies:latest .

    Use a multistage build. A multistage build allows you to create a separate image for each stage of the build process. This can be useful for caching dependencies, as you can create a separate image for the dependency resolution phase. For example, your Dockerfile could look like this:

FROM maven:latest AS builder

COPY pom.xml .

RUN mvn dependency:resolve

FROM openjdk:latest

COPY --from=builder target/

RUN mvn compile install

The first stage of the build will resolve the dependencies and store them in the target/ directory. The second stage of the build will copy the dependencies from the first stage and then compile and install the project.

    Use a Docker volume. You can also use a Docker volume to cache dependencies. This can be useful if you are using a CI/CD system to build your project, as you can mount the same volume to each build job. For example, your Dockerfile could look like this:

FROM maven:latest

COPY pom.xml .

VOLUME ["/root/.m2/repository"]

RUN mvn dependency:resolve -DofflineMode=true

RUN mvn compile install

The VOLUME directive will mount the directory /root/.m2/repository to the container. The first time the build runs, Maven will download the dependencies to this directory. On subsequent builds, Maven will use the cached dependencies, which will save time.

Which measure you choose will depend on your specific needs and environment. If you are using a CI/CD system, then using a Docker volume is probably the best option. If you are building your project locally, then you can use either a cached image or a multistage build.

In addition to the above measures, you can also reduce build time by:

    Using a faster Docker host. If your Docker host is slow, this will impact build time. You can try using a faster machine or cloud-based Docker service.
    Using a lightweight base image. The base image that you choose can also impact build time. Try using a lightweight base image, such as Alpine Linux.
    Optimizing your Maven build. There are a number of things you can do to optimize your Maven build, such as using multiple threads and disabling unnecessary plugins.

By following these tips, you can significantly reduce the build time of your Maven project in Docker.



Q23 :  Why we need multi branch pipeline?
- ans :

Multi-branch pipelines in Jenkins are valuable for managing and automating the continuous integration and continuous delivery (CI/CD) processes for projects that have multiple branches in their version control repositories (e.g., Git, Mercurial). Here are some reasons why multi-branch pipelines are beneficial:

1. **Automated CI/CD for Branches:** With multi-branch pipelines, you can configure Jenkins to automatically create pipelines for each branch in your version control repository. This means that every branch can have its own CI/CD pipeline without the need to manually configure and maintain separate Jenkins jobs for each branch.

2. **Branch Isolation:** Each branch's pipeline operates independently, ensuring that changes and tests for one branch do not interfere with others. This isolation is crucial when working on multiple features or bug fixes simultaneously.

3. **Efficient Resource Utilization:** Multi-branch pipelines make efficient use of resources by running builds and tests only for the branches that have new commits. This prevents unnecessary builds and saves time and resources.

4. **Automatic Branch Detection:** Jenkins can automatically detect new branches and pull requests in your version control repository and create corresponding pipelines. This ensures that CI/CD processes are applied consistently across all branches without manual intervention.

5. **Visibility and Traceability:** Multi-branch pipelines provide clear visibility into the build and deployment status of each branch. Developers can easily monitor the health of their branches and track the progress of builds and tests.

6. **Automatic Environment Provisioning:** You can configure multi-branch pipelines to automatically provision the necessary build and test environments based on the branch's requirements. For example, feature branches may require specific configurations that differ from the main branch.

7. **Parallel Testing:** For projects with many branches, multi-branch pipelines allow you to run tests in parallel for different branches, speeding up the feedback loop and reducing overall build times.

8. **Historical Data and Metrics:** Each branch's pipeline generates historical data and metrics, allowing you to track the evolution of code quality, test coverage, and deployment success over time for each branch.

9. **Support for GitFlow and Feature Branch Workflows:** Multi-branch pipelines are particularly useful for projects following GitFlow or feature branch development workflows, where multiple branches (e.g., feature branches, release branches, hotfix branches) are actively maintained.

10. **Branch-Specific Configuration:** You can define branch-specific configuration parameters for each pipeline, tailoring the CI/CD process to the unique requirements of each branch.

In summary, multi-branch pipelines streamline the management of CI/CD processes in projects with multiple branches, providing automation, isolation, and efficient resource usage. They help development teams maintain a high level of quality and productivity across all branches while reducing manual configuration and intervention.

We need multibranch pipelines for the following reasons:

    To automate the build, test, and deployment of code for multiple branches of a repository. This can be useful for teams that use a branching strategy such as feature branches or git flow. With a multibranch pipeline, Jenkins can automatically create a new pipeline job for each branch that contains a Jenkinsfile. This eliminates the need to manually create and manage pipelines for each branch.
    To ensure that all branches are built and tested in a consistent manner. Multibranch pipelines can be configured to run the same stages and tasks for all branches, regardless of the changes that have been made to the code. This helps to ensure that all branches are in a deployable state.
    To provide feedback to developers on the quality of their changes. Multibranch pipelines can be configured to run automated tests and code analysis tools. This feedback can help developers to identify and fix problems early on, before they are merged into the main branch.
    To improve the speed and efficiency of the development process. By automating the build, test, and deployment process, multibranch pipelines can help teams to release new features and bug fixes more quickly.

Here are some specific examples of how multibranch pipelines can be used:

    A team developing a web application might use a multibranch pipeline to build, test, and deploy their code to different environments, such as development, staging, and production. This would allow them to quickly and easily test new features and bug fixes in a staging environment before deploying them to production.
    A team developing a mobile app might use a multibranch pipeline to build and test their code for different platforms, such as iOS and Android. This would allow them to release their app to both platforms simultaneously.
    A team developing a continuous integration and continuous delivery (CI/CD) pipeline might use a multibranch pipeline to build, test, and deploy their code to different environments, as well as to run automated tests and code analysis tools. This would help them to ensure that their code is of high quality and that it is ready to be deployed to production.

Overall, multibranch pipelines are a powerful tool that can help teams to improve the speed, efficiency, and quality of their software development process.

-----------------

Q24 :  If you forget Jenkins password, how would you login back?
- ans :
If you forget the Jenkins admin password, you can reset it by accessing the Jenkins server's file system and following these steps:

1. **Access the Jenkins Server:**
   - You'll need direct access to the Jenkins server's file system. This can be done by logging into the server directly or through SSH.

2. **Locate the `secrets` Directory:**
   - Navigate to the Jenkins home directory on the server. The Jenkins home directory is typically `/var/lib/jenkins` on Linux systems.
   - Inside the Jenkins home directory, locate the `secrets` directory. You can typically find it at `/var/lib/jenkins/secrets`.

3. **Reset the Password:**
   - In the `secrets` directory, you should find a file named `initialAdminPassword`.
   - To reset the Jenkins admin password, you can simply delete or rename the `initialAdminPassword` file. For example:

     ```bash
     sudo rm /var/lib/jenkins/secrets/initialAdminPassword
     ```

   - Deleting this file will trigger Jenkins to generate a new admin password on the next Jenkins startup.

4. **Restart Jenkins:**
   - After deleting the `initialAdminPassword` file, restart the Jenkins service:

     ```bash
     sudo systemctl restart jenkins  # On systemd-based systems
     ```

   - Alternatively, use the appropriate command to restart Jenkins on your system.

5. **Retrieve the New Password:**
   - Wait for Jenkins to restart completely. This may take a few moments.
   - Once Jenkins is up and running, access the Jenkins web interface using your server's IP address or domain name and port 8080 (e.g., http://your-server-ip:8080).
   - You should see a page that prompts you to unlock Jenkins. To retrieve the new admin password, follow the on-screen instructions.

6. **Unlock Jenkins:**
   - Jenkins will provide you with a path to the location of the new admin password file. Typically, this is found in the Jenkins server's logs. You can access it by running:

     ```bash
     sudo cat /var/log/jenkins/jenkins.log
     ```

   - Look for a line that contains the new admin password. It will look something like this:

     ```
     *************************************************************
     *************************************************************
     *************************************************************

     Jenkins initial setup is required. An admin user has been created and a password generated.
     Please use the following password to proceed to installation:

     1a2b3c4d5e6f7g8h9i0j

     This may also be found at: /var/lib/jenkins/secrets/initialAdminPassword

     *************************************************************
     *************************************************************
     *************************************************************

     ```

   - Retrieve the new admin password from the logs or the file mentioned in the message.

7. **Complete the Setup:**
   - Copy the new admin password and paste it into the Jenkins web interface to complete the setup.

After following these steps, you should be able to log in to Jenkins with the new admin password. Be sure to store the new password securely.



-------------------------------------
--------------
--------------
----------------

# Docker

Q26 : Any best practices for docker ?
- ans :

There are several best practices for performance, security, manageability , reliability and availability.

1. whenever creating a customized images :
- Always start with a minimal base image that contains nexessary components for application to run.
- always use official docker images from trusted sources.
- use the images  having upsated security.
- reduce number of layers to improve build and runtime performance
- Use multistage builds to create smaller images by copying necessary files. and removing intermediate files.
- regularly update the base image to include security update
- avoid running container as root user.
- grant container only the necessary priviledges
- should use image scanning tools to identify vulnerabilities in images
- use docker compose for multi container applications we can define all the servoces and dependencies in a single YAML file,
- Allocate appropriate CPU and memory resources to containers based on their requirements, we can update resource limits and reservation to prevent resource contentation
- use docker system prune regualry to remoe unused container images and volumes to freeup disk space 
- we should run only one rocess in a container .This makes it easier to scale, manage, and troubleshoot containers.
- we should not hardcode configurations values inside container images, we should provide these values using envt variables
- can implement health check eg liveness and readiness probe
- should enable monitoring and enable log retention , life cycle policies.
- use docker volumes and persistent data.
- avoid storing imp data inside container
- version the image and  use tagging
- we should implement disaster and backup recoveryfor data stored in container volumes
- document everything 
- automate the container lifecycle using the container orchestration tools to automate deployement, scaling, etc
- optimize the caching for image layers when building the images
- use .dockerignore file to ignore files that need not to be in container


---------------------------

Q27 : Difference between docker kill and docker stop ?
- ans :

In Docker, both `docker stop` and `docker kill` commands are used to stop running containers, but they differ in their behavior and the signals they send to the container. Here's the difference between `docker stop` and `docker kill`:

### 1. **`docker stop`:**
- **Command:**
  ```bash
  docker stop [OPTIONS] CONTAINER [CONTAINER...]
  ```
- **Behavior:**
  - Gracefully stops the running container by sending a `SIGTERM` (terminate) signal.
  - Allows the container process to perform cleanup operations, such as saving state or releasing resources, before shutting down.
  - The container is given a default timeout period (10 seconds) to stop gracefully. If the container doesn't stop within this period, a `SIGKILL` signal is sent.
- **Example:**
  ```bash
  docker stop my_container
  ```

### 2. **`docker kill`:**
- **Command:**
  ```bash
  docker kill [OPTIONS] CONTAINER [CONTAINER...]
  ```
- **Behavior:**
  - Forcibly kills the running container by sending a `SIGKILL` (kill) signal.
  - Does not allow the container process to perform any cleanup operations.
  - Immediately terminates the container without waiting for any running processes to gracefully shut down.
- **Example:**
  ```bash
  docker kill my_container
  ```

### Key Differences:

1. **Signal Sent:**
   - `docker stop` sends a `SIGTERM` signal, allowing the container to perform cleanup operations.
   - `docker kill` sends a `SIGKILL` signal, forcefully terminating the container without giving it a chance to perform cleanup.

2. **Graceful Shutdown:**
   - `docker stop` allows for a graceful shutdown, giving the container a chance to clean up before termination.
   - `docker kill` does not allow for a graceful shutdown; it immediately terminates the container.

3. **Timeout:**
   - `docker stop` has a default timeout period (10 seconds) for the container to stop gracefully. If the container doesn't stop within this period, a `SIGKILL` signal is sent.
   - `docker kill` does not have a timeout; it forcefully terminates the container immediately.

### Usage Guidance:

- Use `docker stop` when you want to allow the container to perform cleanup operations before stopping. This is the recommended way to stop containers in most cases.
  
  ```bash
  docker stop my_container
  ```

- Use `docker kill` when you need to forcefully and immediately terminate the container, without allowing it to perform any cleanup operations. This is more aggressive and should be used judiciously.

  ```bash
  docker kill my_container
  ```

In summary, the choice between `docker stop` and `docker kill` depends on the desired behavior and whether you want to allow the container to gracefully shut down or forcibly terminate it.

------------------------


Q28 : command to list containers which state is exited ?
- ans :

To list Docker containers that are in an "exited" state, you can use the `docker ps` command with the `--filter` option to filter containers based on their status. The following command lists all containers that are in the "exited" state:

```bash
docker ps --filter "status=exited"
```

Explanation:

- `docker ps`: Lists containers.
- `--filter "status=exited"`: Applies a filter to show only containers with the specified status, which in this case is "exited."

This command will display information about containers that have exited, including their container ID, names, and exit status. If you want more detailed information about the exited containers, you can use the `docker ps -a` command with the same filter:

```bash
docker ps -a --filter "status=exited"
```

Adding the `-a` flag includes stopped containers in the listing.

Remember that containers in the "exited" state are not actively running but may have been stopped for various reasons. You might want to check the exit codes and logs for further information:

```bash
docker logs <container_id>
```

Replace `<container_id>` with the actual ID of the exited container.

-----------------------------


Q29 : command to cleamup docker host ( deleting stopped containers, dangling images and unused networks ) ?
- ans :

To clean up a Docker host by deleting stopped containers, dangling images, and unused networks, you can use the following command:

```bash
docker system prune -a
```

Explanation:

- `docker system prune`: This command is used to clean up Docker resources on the host.
- `-a`: It removes all unused images, not just dangling ones. This includes both dangling images (those not associated with a container) and unreferenced images (those not associated with an existing image).

Alternatively, you can use individual commands to clean up specific types of resources:

1. **Delete Stopped Containers:**
   ```bash
   docker container prune
   ```

2. **Delete Dangling Images:**
   ```bash
   docker image prune
   ```

3. **Delete Unused Networks:**
   ```bash
   docker network prune
   ```

Using `docker system prune -a` is a convenient way to perform a comprehensive cleanup, removing multiple types of unused resources in one command. However, it's essential to be cautious when using the `-a` option, as it will remove all unused images, not just dangling ones. Ensure that you won't unintentionally remove images that are still in use.

Remember that these cleanup commands irreversibly remove resources, so use them with caution, especially in a production environment. Always verify the impact of cleanup commands before running them on a production system.

--------------------------------------

Q30 : What version of docker you have used ? , specific reason to use that perticular version ?
- ans :

The specific version of Docker that I have used depends on the project that I am working on. However, I have used a variety of Docker versions, including:

* Docker 20.10: I used this version of Docker because it added support for containerd 1.4, which is a more performant and stable container runtime.
* Docker 23.03: I am currently using this version of Docker because it has further improvements to performance and stability, as well as new features such as support for building images from Dockerfiles that are written in Rust.



I have also used a number of other versions of Docker, including older versions and newer versions than the ones I have listed here.

The specific version of Docker that I use depends on the project that I am working on. I always try to use the latest stable version of Docker, but I may sometimes use an older version if there is a specific reason to do so. For example, I may use an older version of Docker if I am working on a project that requires a specific feature that is not available in the latest version of Docker.


-----------------

Q31 : can we have multiple CMD in Dockerfile ?
- ans :


In a Dockerfile, you can have only one `CMD` instruction. The `CMD` instruction specifies the default command to be executed when a container is run. If multiple `CMD` instructions are provided in a Dockerfile, only the last one will take effect, and the previous ones will be overridden.

Here's an example of a Dockerfile with multiple `CMD` instructions:

```Dockerfile
FROM ubuntu:latest

# CMD instruction - this will be overridden by the next CMD
CMD ["echo", "First CMD instruction"]

# Another CMD instruction - this will be the effective CMD
CMD ["echo", "Second CMD instruction"]
```

In the example above, only the second `CMD` instruction will take effect when a container is run. The first one will be ignored.

If you need to specify multiple commands or need more complex startup behavior, you can use a shell to run multiple commands. For example:

```Dockerfile
FROM ubuntu:latest

# CMD instruction using a shell - runs multiple commands
CMD echo "First command" && echo "Second command"
```

or we can use a script.

This way, you can achieve the effect of running multiple commands, but it is executed within a shell.

It's worth noting that the `CMD` instruction is often used for specifying the default command and parameters for the container, but it can be overridden at runtime by providing a command when running the container. For example:

```bash
docker run my_image echo "Override CMD with a different command"
```

In this case, the provided command will override the `CMD` specified in the Dockerfile.

-----------------------



Q32 : Have you worked on docker swarm and docker compose ?
- ans :

Yes, I have worked on both Docker Swarm and Docker Compose. They are both container orchestration tools that can be used to manage clusters of Docker containers.

**Docker Swarm** is a container orchestration tool that is built into Docker Engine. It can be used to manage a cluster of Docker Engine instances and to deploy and manage applications on the cluster. Docker Swarm is a good choice for organizations that need a powerful and flexible container orchestration tool.

**Docker Compose** is a tool that can be used to define and run multi-container Docker applications. It is a good choice for organizations that need a simple and easy-to-use tool for deploying and managing multi-container applications.

I have used both Docker Swarm and Docker Compose to deploy and manage applications in production environments. I have found that both tools are effective and reliable. The best tool for a particular use case will depend on the specific requirements of the organization.







----------


------------
----------
-----------------------

# Kubernetes

Q33 : Can we have multiple conatiners in a pod?
- ans :
- 
architect link : https://www.linkedin.com/pulse/multi-container-init-container-pod-kubernetes-prachika-kanodia-

Yes, in Kubernetes  we can run multiple containers within a single pod. A pod is the smallest deployable unit in Kubernetes, and it can contain one or more containers that share the same network namespace, storage volumes, and some other resources. it is commonly used for various purposes, such as co-locating containers that work together as part of a single application or including sidecar containers for tasks like logging, monitoring, or data synchronization.

The primary reason that Pods can have multiple containers is to support helper applications that assist a primary application. however it will be a tightly coupled architecture and we are handling it as a single unit which is not a good practice.



Example manifest file : 
```
apiVersion: v1
kind: Pod
metadata:
  name: multi-container-pod
spec:
  containers:
  - name: web-server
    image: nginx:latest
  - name: logging
    image: fluentd:latest
    volumeMounts:
    - name: log-volume
      mountPath: /var/log
  volumes:
  - name: log-volume
    emptyDir: {}

```

Few pros of this are effeciency since it shares the same resources and dependencies it can imrove performance and reduces cost.

communication using the same network namespaces is easy and no hard network configurations needed however if one container is vulnerable then hacker can access data for  other containers as well.

Management ans scaling is very easy as the whole stack is in single pod.

Generally we use this approach in : 
    A web server pod with a sidecar container that handles logging.
    A database pod with a sidecar container that provides backup and recovery functionality.
    A microservices pod with multiple containers that provide different pieces of functionality.

----------------------

Q34 : Can we have similar conatiners in a pod? Lets say i have 4 conatiners, one of them has failed how would you check which container has failed?
- ans :

Yes, we can have multiple containers running within a single podin k8. this is useful for running multiple instances of same application or for running different application that share same resources. these containers share the same network namespaces and can communicate with each other via localhost. These containers can be same or different like sidcar containers for logging , monitoring,  or other tasks.

if we have multiple containers in pod and one of them is failed then we can determine using : 


we can filter the results if we have so many containers .
` kubectl get pod <podname> -o=jsonpath='{range .status.containerStatuses[*]}{.name}{"\t"}{.ready}{"\t"}{.state.waiting.message}{"\n"}{end}' `


logs for specific container within a pod ` kubectl logs <pod-name> -c <container-name>`

or using the pod status ,if one of the container has failed the pod status will reflect this. we can see "Error" or "CrashLoopBackOff" state.

`kubectl get pods`

Using the events also we can find that. we can get the detailed info about pods and its containers and we can check event section  for any event related to container failures.
`kubectl describe pod <pod-name>	`

events `kubectl get events --field-selector involvedObject.name=<pod-namw>`

other than this if we  have configured monitoring and alerts that may work as well. we can also use k8 dashboard for the same.


---------------------------------

Q35 : What is liveness and readiness probe? Why we need them?
- ans :
Liveness and readiness probes in k8  is essential to get the reliability and availability of applications  running in containers, both are for  differnt purposes i.e health anf readiness of pods.

Liveness porbe :
Liveness porbe is used to determine whether a container within a pod is alive and healthy. it helps k8 to identify and restart containers that are crashed or non responsive state,

so how exactly it works ,  liveness probe periodically sends a request to a specified endpoint (HTTP, TCP socket, or an arbitrary command) within the container. If the container responds successfully (e.g., returns a 200 OK HTTP status code or the command exits with a success status), Kubernetes considers the container to be healthy. If the probe fails after a certain number of consecutive attempts, Kubernetes restarts the container. If a liveness probe fails, Kubernetes will restart the container

It is mainly used to recover from situations where a container may have entered a deadlock state , or become unresponsive due to resource constraints , or container crashed etc. It mainly helps us to identify which endpoints are available to serve traffic and improve availability.


Readiness Probe : 
Readiness porbe is used to determine whether a container is ready to accept incoming traffic and server requests, and pods should not handle the traffic untill the application is ready.  If a readiness probe fails, Kubernetes will not route traffic to the container

 Similar to the liveness probe, the readiness probe sends requests to a specified endpoint within the container. If the probe succeeds, the container is considered ready. If it fails, the container is marked as not ready, and Kubernetes removes it from service until it passes the probe again.

It is used to prevent traffic from being sent to containers that are still initializing , starting or in the process of loading application dependencies


We need both readiness and liveness for improving availability, traffic control, resource effeciency, and graceful startup and shutdown. both health checks may run at regular intervals and if probe fails k8 can take corrective actions such as restarting container or stopping traffic from being routed

probes can be configured for containers in Kubernetes deployments and daemon sets.
Example :


```yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx-container
    image: nginx
    ports:
    - containerPort: 80
    livenessProbe:
      httpGet:
        path: /nginx-health/live
        port: 80
      initialDelaySeconds: 3
      periodSeconds: 5
    readinessProbe:
      httpGet:
        path: /nginx-health/ready
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 10
    startupProbe:
      httpGet:
        path: /nginx-health/startup
        port: 80
      initialDelaySeconds: 10
      periodSeconds: 10
      failureThreshold: 30
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: NodePort

```


-----------------

Q36 : Have you worked on kubernetes monitoring? Which tools you have used?
- ans :
K8 cluster monitoring is one of the main process to ensure health , performance, and reliability of containerized application, there are various open source and managed platforms available for both on prem and cloud k8 clustor monitoring.

Prometheus :  it is open source monitoring and alerting tool we can set prometheus to scrape metrics from k8 nodes , pods and services and if there is any issue it can trigger an alert this functionality is provided by alertmanager,
prometheus also provides custom libraries which extends the funtionaliyu or we can use open telemetry to gain deeper insights into application peroformance 

Grafana : we can use grafana with prometheus for custom dashboard ,  we can create  new dashboard or download dashboard i.e json file, it has user fiendly interface and we can easily monitor overall health and performance and can share the dashboards as well.

Kube state metrics : it is k8 tool to gain insights into state of k8 objects such as deployment, pods and services. k8 dashboard is also available it is web based ui and provides overview of k8 cluster. it can be  used to monitor health of nodes,pods,services. kubewatch is also available it is an event minitor for k8 cluster. we can use to monitor for events such as pod creation ,termination ,node outage, service failure etc.

CAdvisor : to monotor the container cadvisor is a good tool by google, it collects detailed performance metrics for containers like cpu usage, memory utilization, network statistics etc depends on what kind of container we deployed.

we can also use elasticsearh, fluentd and kibana i. EFK Stack to capture and analyze logs  and there are other tools as well like jaeger or zipkin for distributed tracing across microservices in k8. Jaeger is a good tool for monitoring because it allows us to see how requests are flowing through our application and identify performance bottlenecks



These monitoring solutions generates data and we also have logs alredey generationg  for this we can use the retenetion policies or lifecycle policies.




---------------

Q37 : Can we deploy a pod on particular node?
- ans :

Yes, we can deploy a pod in particular node in k8 cluster by using node affinity, node selector, taints and tolerations, or using nodename field.

We can use node affinity which allows us to restrict on which node our pod is eligible to schedule based on  node labels. and we can set up affinity rules to deploy a pod on nodes with specific labels.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: static-web
  labels:
    role: myrole
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: kubernetes.io/hostname
            operator: In
            values:
            - k8s-worker1
  containers:
    - name: web
      image: nginx
      ports:
        - name: web
          containerPort: 80
          protocol: TCP

```

we can also use node selector to schedule pod on specific node with specific label.

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: static-web
  labels:
    role: myrole
spec:
  nodeSelector:
    kubernetes.io/hostname: k8s-worker1
  containers:
    - name: web
      image: nginx
      ports:
        - name: web
          containerPort: 80
          protocol: TCP


```

we can also use taint and tolerations , taints allows nodes to repel pods and tolerations allows pods to tolerate certain limits  by applying these we can deploy pods on particular nodes.

```bash
kubectl taint nodes <node-name> <taint-key>=<taint-value>:NoSchedule
kubectl taint nodes k8s-worker1 mytaint=example:NoSchedule


```
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: static-web
  labels:
    role: myrole
spec:
  containers:
    - name: web
      image: nginx
      ports:
        - name: web
          containerPort: 80
          protocol: TCP
  tolerations:
    - key: mytaint
      operator: Equal
      value: example
      effect: NoSchedule

```

we can also specify nodename field directly in the pod definition .
```yaml


apiVersion: v1
kind: Pod
metadata:
  name: static-web
  labels:
    role: myrole
spec:
  nodeName: k8s-worker1
  containers:
    - name: web
      image: nginx
      ports:
        - name: web
          containerPort: 80
          protocol: TCP

```


-----------------------
















