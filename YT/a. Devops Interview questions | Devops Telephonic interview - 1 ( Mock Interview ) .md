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





---------
---------

Q6 : How to clone specific branch in  git ?
- ans :



-------------------------

Q7 : When i issue mvn install what all things happen in background ?
- ans :

Q8 : Do you know what is .m2 folder ?
- ans :

Q9 : what are the settings you need to do in pom.xml or any other settings you need to do before running mvn in deploy ?
- ans :

Q10 : have you build any maven projects in local ? if you to maven build first time it takes less time to build and next time it will takes less time to build, why it happens ?
- ans :


----------------------------

Q11 : how to get present working folder ? 
- ans :

Q12 : how to copy files from local windows machine to cloud based linux machine , suppose i dont have any admin access ?
- ans :

Q13 : a shell script named test.sh can acept 4 parameters i.e a,b,c,d that parameters wont supplied in order always and number parameters might also vary ( only 2 parameters user might supply sometimes), how to identify position of letter c ?
- ans :



-----------------------

Q11 : Have you worked on adhoc command ?
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
















