## Devops Interview questions | Devops Telephonic interview - 2 ( Mock Interview ) 
* mock : https://www.youtube.com/watch?v=lXGAJElFxaA&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=2
* Answers : https://www.youtube.com/watch?v=7WJ31VFk1_Y&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=10
  
------------------------------------

Q1 : Can you tell me what are tools you have used and your daily activities ?
-ans :

-----------
----
----

Q2 : What work have you did in git like only related to devops or other as well ?
-ans :

I have worked mostly on git push and pull , clone , fetch , as I worked as devops engineer, most of the admin activities were performed by the developer or the repo admins they used to perform admin activities like access control, repository management, branching strategies, code reviews , issue tracking, backup n recovery, git maintenance, compliance and security, got hooks .

I have worked on GitHub webhook, whenever there's a commit a jenkins job used to trigger , and I have created pat token for the Authorization by selecting the correct permissions. GitHub webhook is nothing but an api request. It send tha data i.e http post and send some json payload to the endpoint we have configured. There are various api protocols like grpc , http, UDP , TCP here it uses http protocol for the communication and here it performance two way handshake let's suppose it sends some data to jenkins, jenkins will reply back as the data has been received and triggers the job by fetching the changs.

I have also migrated the GitHub repo to code commit. Here we need to create a repo in code commit then need to clone in the local laptop or whatever machine we are using, while cloning we may need some permission to access the code commit repo for this we can use iam role attached to vm in case our machine is ec2 or we can create AWS iam user by giving proper set of permissions. Then we can clone the code commit repo we also need to clone gitrepo if the repo is private we may need pat token then update the config file i.e located in .git folder where we need to update origin url or we can use the command to update origin url , a better way to use the command so we can track the changes by AWS Cloudwatch agent or any other monitoring agent if we are using.

After updating the origin url we can push the repo to code commit here we need to make sure every branch is pushed. We can use command to push all branches or if we have so many branches we can use a script to do that aswell , script may include a loop to push the branch one by one.

In azure the migration is very simple as git is owned by Microsoft only we just need to enter the git url and pat token and by using import option the whole git repo will be migrated.

For Oracle also we need to follow the steps like AWS.

when setting up webhooks or migrating repositories, it's crucial to consider security measures. For GitHub webhooks, using a secret token and verifying the HMAC signature of incoming payloads helps ensure data authenticity. also the pat token should be stored in key vaults of the respective cloud services AWS Azure Oracle considering the sensitivity. and while configuring the roles of giving permissions we should follow the rbac and least privileged.


*************** NEW ANSWER HERE *************************** 

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

We can do this using the shllow clone. 
We can clone a single branch using the flag `--single0branch` however it will clone only master or main branch if we need to specify a particulra branch we can using `--branch <branch name>` to clone the particukar branch the we need to use `--depth  1` to clone only last commit.

So the command willl look like this :
```
# Clone the repository (only the 'master' branch with the latest commit)
git clone --single-branch --branch master --depth 1 "$REPO_URL" "$CLONE_DIR"

``` 

The `--depth ` option is like a tree where the smaller number we provide will give less details lest suppose as leaves of tree , the larger the number it ill go down more providing more details like trunk to root of tree.

After performing shallow clone with limited depeth if there is any update in the repository we can use   `git fetch origin master`  and `git reset --hard origin/master`   here we canupdate it to the latest commit .

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

2.   Reducing bandwith : If e are using EC2 for develeopers , indeed we have incoming traffic free however the utgoing traffic will have charges depending on the bandwith  , ampiunt of data transfer so fetchng onu required data will help us to mantain te cost as well , ets suppose we are creating a jenkins job then a container or storing / archiving th artifact or pushing to git repo all these are outgoing traffic .  and gere we can save a cost , This can be helpful when we have 1000s of devs , testers etc.

3.  cloning single repo with less deothe can also be helpful for automateed  code reviews, automated tasks ,    and we can easily manage large repositories.




----
----

 

Q6 : what is submodule and why we need submodule?
-ans :

Git Submodule is a mechanism whih allows us to include one git repo as a subdirectory withib another git repository.

so we are nesting the repositories here, One git repo i.e submodule is nested  inside nother git repo i.e Superproject.


it is easy way to manage an version control external dependencies or libraries withih the project.
















----
----

 

Q7 : Lets say you have changed 5 files a,b,c,d and e in a repo and you did git add ., now all the files are in staging area, now i decided not to commit file d. how would delete it from staging area?
-ans :











----
----


Q8 :  what is multi module project in maven and what are the setting you want to do in multi module parent and child project ? what is dependency management ?
-ans :

Q9 : what is transitive dependency ?
-ans :

Q10 : Have you worked on commit based job in jenkins? what settings you need to do in jenkins and github to setup commit based job?-ans :
-ans :

Q11 :  you want to create 50 freestyle jobs with same configurations, but only change is job name. how would you achieve teh same?
-ans :

Q12 :  write a script which accepts file or folder, if its folder delete it else print "this is a file"?
-ans :

Q13 : How to check whether particular port is already in use or not ?
-ans :

Q14 : Logic for checking whether supplied string for a script is palindrome or not? what are all the commands you will use ?
-ans :

Q15 :  command to get number of lines in a file ? 
-ans :

Q16 : Lets say i have 4 machines consider 1 as ansible master other 3 as nodes, what are the basic setup you need to do for ansible cluster?
-ans :

Q17 : what are ansible roles? why we need ansible roles? have you worked on ansible galaxy?
-ans :

Q18 : Have you worked on ansible galaxy ? what is ansible galaxy ?
-ans :

Q19 :  What are ansible facts?
-ans :

Q20 : Can we have windows machine as ansible master? as node?have you worked on any windows modules? can you list few?any extra configuration do we need to do ?
-ans :


Q21 : Have you worked on docker save , docker load ?
-ans :

Q22 :  Have you worked on multi-stage dockerfile and why we need that?
-ans :

Q23 : Lets say i have container which is attached with a volume, if container crashes what happens to volume?
-ans :

Q24 : Can you copy a file from local to running containers ?
-ans :

Q25 : what is init container and side-car container?can you give simple scenario where we use these conatiners?
-ans :

Q26 : which one is default deployment strategy? how it works?
-ans :

Q27 :  command to check the container logs in pod?
-ans :

Q28 : what are the types of services present in kubernetes?
-ans :

Q29 : What is the link between pod and service?
-ans :
