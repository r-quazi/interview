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

----
=======

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

--------------



Q28 : what are the types of services present in kubernetes?
-ans :

Kubernetes offers several types of services to expose applications and manage network communication within a cluster. The common types of services in Kubernetes are:

1. **ClusterIP**:
   - **ClusterIP** services provide internal network communication within the cluster. They expose the service on a cluster-internal IP address, allowing other pods within the cluster to access it. These services are not accessible from outside the cluster.

2. **NodePort**:
   - **NodePort** services expose the service on a static port on each node's IP address. They make the service accessible from outside the cluster. When traffic is directed to a node's IP and the defined port, the service forwards it to the appropriate pod.

3. **LoadBalancer**:
   - **LoadBalancer** services are used to expose services to the outside world through cloud provider-specific load balancers. They distribute external traffic to the pods behind the service, making it suitable for scenarios where you need to load balance and provide high availability for external access.

4. **ExternalName**:
   - **ExternalName** services provide a way to map a service to a DNS name. These services do not have selectors or endpoints but instead redirect DNS queries to a specified external DNS name.

5. **Headless**:
   - A **Headless** service, when created with the `ClusterIP: None` setting, does not allocate a cluster-internal IP or provide load balancing. It is used for scenarios where you need direct DNS-based pod-to-pod communication within a service without a single entry point.

6. **Ingress**:
   - An **Ingress** resource is not exactly a service, but it manages external access to the services in your cluster. Ingress controllers can be used to configure rules for routing external traffic to specific services based on HTTP or HTTPS routes.

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

    Label selector: A service uses a label selector to identify the pods that it should proxy traffic to. The label selector can be based on any label that is applied to the pods.
    Endpoints: A service is backed by a set of endpoints, which are the actual pods that the service will proxy traffic to. The endpoints are discovered by the Kubernetes service proxy, which is responsible for load balancing traffic to the pods.

When a client sends traffic to a service, the Kubernetes service proxy intercepts the traffic and forwards it to one of the pods that is backing the service. The service proxy uses a load balancing algorithm to distribute traffic evenly across the pods.

The link between pods and services is essential for running reliable and scalable applications on Kubernetes. Services allow you to expose your application to the outside world without having to worry about managing the individual pods that are backing the service. Services also provide load balancing and failover capabilities, which ensure that your application is always available, even if some of the pods that are backing it fail.

Here is an example of how a service is linked to pods:
```
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

kubectl apply -f service.yaml

Once the service is deployed, you can access it from outside the cluster using the service's IP address. The Kubernetes service proxy will load balance traffic to the pods that are backing the service.
Benefits of linking pods and services

Linking pods and services has a number of benefits, including:

    Abstraction: Services provide an abstraction layer that hides the complexity of managing individual pods. This makes it easier to develop and deploy applications on Kubernetes.
    Load balancing: Services provide load balancing capabilities, which distribute traffic evenly across the pods that are backing the service. This improves the performance and reliability of your application.
    Failover: Services also provide failover capabilities. If a pod fails, the service will continue to proxy traffic to the remaining pods. This ensures that your application is always available, even if some of the pods that are backing it fail.
    Scalability: Services make it easy to scale your application up or down. You can simply add or remove pods from the service, and the service will automatically update its endpoint list. This makes it easy to scale your application to meet the changing demands of your users.
