##  Devops Interview questions | Devops Telephonic interview - 6 ( Mock Interview ) 
https://www.youtube.com/watch?v=Z_bbozP6ZW4&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=6

-------------------------------------------------------

1. What are the tools you have used and please elaborate your day to day activities ?




2. What is Continous integration Continous delivery and Continous deployment ?

## GIT :


3. which version of git you used ?


```
- used latest 3.11 version
- stable , compatible, security update. new fetaures
- git --version
- git update go through porting guide
- other versions used also preinstalled in VMs, 

```

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



```
- both used to integrate changes from one to other branch , diff. approach to combine branch history
- Git Merge :
- creates new merge commit that has 2 parent commit
- creates linear commit hstory ,preserves complete history of both branches
- merged branches maintain their original cmmit history
- generally used with feture branch `   git merge branch_name`


- Git Rebase :
-  used to incorporate changes from one branch into another by moving or reapplying commits from the source branch onto the tip of the target branch.
- rewrites the commit history of the source branch
-  may alter commit timestamps and commit hashes
- `  git checkout feature_branch ` --> ` git rebase target_branch`


- Use `git merge` when you want to preserve the original branch's commit history and create a merge commit to signify the merge.
- Use `git rebase` when you want a linear and cleaner commit history but are willing to rewrite commit history.
```
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



```
- **Squashing Commits:**
  - Technique to combine multiple commits into a single, meaningful commit.
  - Often done before merging feature branches into the main branch.
  - Utilizes interactive rebase for the process.

- **Interactive Rebase Steps:**
  1. Checkout the target branch: `git checkout feature_branch`
  2. Start interactive rebase for the last N commits: `git rebase -i HEAD~N`
  3. In the interactive editor, change "pick" to "squash" for selected commits.
  4. Save and close the editor.
  5. Edit the commit message for the combined commit.
  6. Save and close the commit message editor.
  7. Complete the rebase process.
  8. Force push if needed when pushing to a remote repository.

- **Benefits of Squashing:**
  - Creates a cleaner and more concise commit history.
  - Especially useful for projects with incremental commits during development.
  - Enhances readability and understanding of the commit history.

- **Comparison with Git Rebase:**
  - Squashing combines multiple commits into one for a cleaner history.
  - Git rebase applies commits on different base commits, forming a new branch.
  - Squashing is typically done on private branches, while rebase can be used on shared branches.

- **Squashing Multiple Commits:**
  - Use `git reset --soft HEAD~N` to reset to the desired commit.
  - Follow with `git commit` to create a new commit, or use `--edit` to concatenate commit messages.

Squashing commits is a valuable practice for maintaining a clean and logical commit history, facilitating easier collaboration and code understanding.


```

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

| Git Squash          | Git Rebase              |
|---------------------|-------------------------|
| You can combine multiple commits into a single commit.  | Applies commits on top of different base commits. |
| After using git squash, your commit history will be more clean and organized. | You can form a new branch by using previous commits. |
| Must be done on private branches. | Rebasing can be done on a feature branch or shared branch. |
| By using squashing, you can maintain a clean and logical commit history. | By using the rebase command, you can keep your branch up to date. |



to squash multiple commits tegether :




You can do this fairly easily without git rebase or git merge --squash. In this example, we'll squash the last 3 commits.

If you want to write the new commit message from scratch, this suffices:

git reset --soft HEAD~3 &&
git commit

If you want to start editing the new commit message with a concatenation of the existing commit messages (i.e. similar to what a pick/squash/squash/…/squash git rebase -i instruction list would start you with), then you need to extract those messages and pass them to git commit:

git reset --soft HEAD~3 && 
git commit --edit -m"$(git log --format=%B --reverse HEAD..HEAD@{1})"

Both of those methods squash the last three commits into a single new commit in the same way. The soft reset just re-points HEAD to the last commit that you do not want to squash. Neither the index nor the working tree are touched by the soft reset, leaving the index in the desired state for your new commit (i.e. it already has all the changes from the commits that you are about to “throw away”).



---------
---------

6. What branching strategy you used and which is good ?



```
- **Feature Branch Workflow:**
  - Each feature or bug fix has a dedicated branch.
  - Feature branches are created from the main branch and merged back when complete.
  - Keeps main branch stable, enables parallel feature development.

- **Gitflow Workflow:**
  - Defines a structured branching model (feature, develop, release, hotfix).
  - Suitable for larger projects with complex release cycles.
  - Provides clear guidelines for different types of development.

- **GitHub Flow:**
  - Emphasizes continuous delivery with a focus on simplicity.
  - Development in feature branches, merged into the main branch.
  - Suitable for rapid development and deployment cycles.

- **Trunk-Based Development:**
  - All development in a single branch (master or main).
  - Focus on keeping the main branch stable at all times.
  - Effective for small teams with high automation and quick releases.

- **GitOps Workflow:**
  - Combines Git with infrastructure as code and automation.
  - Manages infrastructure and application deployments declaratively.
  - Suitable for projects requiring automated infrastructure management.

- **GitHub Flow Strategy:**
  - Uses main for production code and feature branches for development.
  - Encourages small, frequent merges using pull requests.
  - Simple and lightweight, suitable for small to medium-sized teams.


```


The choice of a branching strategy in Git depends on your team's development workflow and the specific needs of your project. There is no one-size-fits-all branching strategy, and what works best can vary from one project to another. Here are a few common branching strategies and when they might be suitable:

1. **Feature Branch Workflow:**
   - In this strategy, each new feature or bug fix is developed in a dedicated feature branch.
   - Feature branches are created from the main development branch (often `master` or `main`) and are merged back into that branch when the feature is complete.
   - This strategy keeps the main branch stable and allows for parallel development of multiple features.

   **When to use:** This is a flexible and widely used strategy suitable for most projects. It keeps the main branch clean and provides isolation for feature development.

2. **Gitflow Workflow:**
   - Gitflow defines a strict branching model with dedicated branches for features, releases, and hotfixes.
   - It introduces branches like `feature`, `develop`, `release`, and `hotfix` in addition to `master` for long-term stability.
   - This strategy is more structured and provides clear guidelines for different types of development and releases.

   **When to use:** Gitflow can be useful for larger projects with complex release cycles and the need for a well-defined process.

3. **GitHub Flow:**
   - GitHub Flow is a simpler strategy that emphasizes continuous delivery.
   - Development happens in feature branches, and once a feature is complete and tested, it's merged into the main branch (usually `main`) and deployed.
   - It encourages smaller, more frequent merges, reducing the time between development and deployment.

   **When to use:** GitHub Flow is suitable for projects where you want to maintain a rapid development and deployment cycle with a strong focus on simplicity.

4. **Trunk-Based Development:**
   - In this strategy, all development happens in a single branch, often `master` or `main`.
   - Developers commit frequently, and the goal is to keep the main branch stable at all times.
   - Continuous integration and automated testing are crucial for ensuring the stability of the main branch.

   **When to use:** Trunk-Based Development is effective for small teams or projects with a high level of automation and emphasis on quick releases.

5. **GitOps Workflow:**
   - GitOps is a strategy that combines Git with infrastructure as code (IaC) and automation to manage infrastructure and application deployments.
   - Changes to the infrastructure and application configurations are stored in Git repositories and automatically applied to the live environment.

   **When to use:** GitOps is suitable for projects that require a declarative and automated approach to managing infrastructure and deployments, such as cloud-native applications.

The choice of a branching strategy should align with your team's workflow, project size, and release cycle. It's important to document and communicate the chosen strategy to ensure that all team members understand how to work with branches and how code is integrated and released. Additionally, it's often beneficial to revisit and adapt your branching strategy as your project evolves and your team's needs change.



I used the GitHub Flow branching strategy for this conversation. This strategy is simple and lightweight, and it is well-suited for small to medium-sized teams. It is also a good choice for teams that work on short-lived projects or that need to release new features quickly.

The GitHub Flow strategy uses two main branches:

    main: This branch contains the code that is currently in production.
    feature: Developers create feature branches to work on new features or bug fixes. Once a feature is complete and tested, it is merged into the main branch.

The GitHub Flow strategy also recommends using pull requests to merge changes from feature branches into the main branch. This allows other developers to review the changes before they are merged, which helps to ensure code quality.

For Devops : https://www.bmc.com/blogs/devops-branching-strategies/







---------
---------
----------


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


## k8 :

--------------------------
--------------------------
24. Are you administring k8 or deploying ?

ans :
"I am primarily focused on deploying applications on Kubernetes. In this role, I work on creating and optimizing CI/CD pipelines for Kubernetes, automating deployments, and managing infrastructure as code. My responsibilities include ensuring proper containerization of applications, managing Docker images, and overseeing the deployment and scaling of applications within the Kubernetes environment."


--------------------------

25. Can we deploy pods on master node ?

ans :

Yes, it is possible to schedule and deploy pods on the master node in Kubernetes. However, it is generally not recommended to deploy application workloads directly on the master node for several reasons:

1. **Security:** The master node is a critical component of the cluster responsible for managing and controlling the entire cluster. Deploying user workloads on the master node might expose them to potential security risks.

2. **Resource Contention:** The master node is responsible for various control plane components, and running user workloads on the same node may lead to resource contention, affecting the performance and stability of the control plane.

3. **High Availability:** Deploying user workloads on the master node may impact the high availability of the control plane components. It's common practice to have multiple master nodes for redundancy and fault tolerance.

That being said, if you still want to deploy a pod on the master node, you can do so by removing taints from the master node or by explicitly tolerating the master node's taints. A taint is a key-value pair applied to a node that prevents the scheduling of pods unless they have a matching toleration.

Here's an example manifest file that deploys a simple Nginx pod on the master node:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
  tolerations:
  - key: node-role.kubernetes.io/master
    effect: NoSchedule
```

In this example:

- The pod is named "nginx-pod" and contains a single container running the Nginx image.
- The `tolerations` section specifies that the pod tolerates the taint with the key `node-role.kubernetes.io/master` and the effect `NoSchedule`. This allows the pod to be scheduled on a node with this taint, which includes the master node.

Keep in mind the considerations mentioned earlier, and use caution when deploying workloads directly on master nodes in a production environment.






--------------------------

26. Have you come across configmap and why we use it ?

ans :

Yes, ConfigMap is a Kubernetes resource used to store configuration data in key-value pairs, allowing you to decouple configuration from application code. ConfigMaps provide a way to manage configuration data and consume it in pods or other resources.

### Why use ConfigMap:

1. **Separation of Concerns:** ConfigMaps separate configuration data from application code, promoting a cleaner separation of concerns. This makes it easier to manage and update configuration independently of the application.

2. **Centralized Configuration:** ConfigMaps provide a centralized location to store and manage configuration data for multiple pods or containers. This is especially useful in scenarios where multiple instances of an application share the same configuration.

3. **Dynamic Configuration Updates:** ConfigMaps allow you to update configuration data dynamically without redeploying the entire application. This is helpful for scenarios where configuration changes frequently or needs to be updated without disrupting the application.

4. **Consistent Configuration Across Environments:** ConfigMaps help ensure consistent configuration across different environments, such as development, testing, and production, by providing a single source of truth for configuration data.

### Manifest File Example:

Here's an example of a ConfigMap manifest file:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: myapp-config
data:
  APP_ENV: "production"
  DB_HOST: "db.example.com"
  DB_PORT: "5432"
  API_KEY: "abc123"
```

In this example:

- `metadata.name`: Specifies the name of the ConfigMap (in this case, "myapp-config").
- `data`: Contains the key-value pairs representing the configuration data.

Once you create a ConfigMap, you can reference it in your pods, deployments, or other resources. Here's an example of a pod manifest file using the ConfigMap:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
  - name: myapp-container
    image: myapp-image:latest
    env:
    - name: APP_ENV
      valueFrom:
        configMapKeyRef:
          name: myapp-config
          key: APP_ENV
    - name: DB_HOST
      valueFrom:
        configMapKeyRef:
          name: myapp-config
          key: DB_HOST
    - name: DB_PORT
      valueFrom:
        configMapKeyRef:
          name: myapp-config
          key: DB_PORT
    - name: API_KEY
      valueFrom:
        configMapKeyRef:
          name: myapp-config
          key: API_KEY
```

In this pod manifest:

- `env`: Defines environment variables sourced from the ConfigMap using `configMapKeyRef`.
- Each key in the ConfigMap corresponds to an environment variable in the pod.

This way, you can manage your application's configuration centrally using ConfigMaps and ensure that your pods have consistent and up-to-date configuration data.



--------------------------

27. What is default deployment strategy in k8 ?

ans :

The default deployment strategy in Kubernetes is known as "RollingUpdate." In a RollingUpdate strategy, the new version of the application is gradually rolled out, replacing instances of the old version one at a time, ensuring that the deployment remains available and stable throughout the process.

Here's an example of a Deployment manifest file with the default RollingUpdate strategy:

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

Explanation of key elements in the manifest:

- `spec.replicas`: Specifies the desired number of replicas (pods) for your application. In this example, it's set to 3 replicas.

- `spec.selector.matchLabels`: Defines the selector that determines which Pods belong to the Deployment.

- `spec.template`: Specifies the Pod template used to create new Pods when scaling or updating the Deployment.

- `spec.strategy`: Defines the deployment strategy. In this case, it's set to "RollingUpdate."

- `spec.strategy.rollingUpdate.maxSurge`: Specifies the maximum number of additional pods that can be created during an update. In this example, one additional pod is allowed beyond the desired replica count.

- `spec.strategy.rollingUpdate.maxUnavailable`: Specifies the maximum number of pods that can be unavailable during the update. In this example, one pod can be unavailable at a time.

- `minReadySeconds`: Specifies the minimum number of seconds for which a newly created pod should be ready without any errors before considering it available. In this example, it's set to 5 seconds.

This RollingUpdate strategy ensures that the deployment proceeds gradually by updating one pod at a time while maintaining a specified number of replicas available and avoiding downtime. Adjust the `maxSurge` and `maxUnavailable` values based on your application's requirements.





--------------------------

28. Have you used helm and why we need helm ?

ans :

Yes, Helm is a widely used package manager for Kubernetes applications. It simplifies the process of deploying and managing applications on Kubernetes by providing a standardized way to define, install, and upgrade applications.

### Why Helm is Used:

1. **Package Management:**
   - Helm allows you to package your entire application, including Kubernetes manifests, configurations, and dependencies, into a single unit called a "chart." This makes it easy to distribute and share applications.

2. **Templating:**
   - Helm uses Go template language to enable parameterization and dynamic configuration of Kubernetes manifests. This makes it simple to customize deployments for different environments without duplicating YAML files.

3. **Reusability:**
   - Helm charts can be shared and reused across projects, teams, and organizations. The Helm Hub serves as a centralized repository of charts that can be easily accessed and deployed.

4. **Versioning and Rollbacks:**
   - Helm enables versioning of charts, allowing you to roll back to a previous version if an update causes issues. This is crucial for maintaining application stability and reliability.

5. **Declarative Configuration:**
   - Helm charts provide a declarative way to define the desired state of your application. This aligns with the Kubernetes philosophy of declarative infrastructure and allows for easy management of complex applications.

6. **Ecosystem and Community:**
   - Helm has a vibrant community and a rich ecosystem of charts for various applications and services. This community-driven approach accelerates the adoption of best practices and provides a wealth of pre-built charts.

### Helm Usage Example:

Here's a brief example of using Helm to install a chart:

1. **Install Helm:**
   - Before using Helm, you need to install the Helm CLI on your local machine. Instructions can be found on the Helm official website: [Get Helm](https://helm.sh/docs/intro/install/).

2. **Initialize Helm:**
   ```bash
   helm init
   ```

3. **Create a Helm Chart:**
   - You can create a new Helm chart or use an existing one. A Helm chart typically includes a `values.yaml` file for configuration and a set of Kubernetes manifest files.

4. **Install the Chart:**
   ```bash
   helm install myapp ./myapp-chart
   ```

   Replace `myapp` with the desired release name and `./myapp-chart` with the path to your Helm chart.

Helm simplifies the deployment and management of applications on Kubernetes, making it an essential tool for anyone working with containerized applications in a Kubernetes environment.








--------------------------

29. how can we find the unised values in helm ?

ans :
To find unused values in a Helm chart, you can use Helm's `lint` command combined with some additional tools. Helm doesn't provide a direct command to identify unused values, but you can achieve this by following these steps:

1. **Lint the Helm Chart:**
   Use the `helm lint` command to identify any issues, including unused or undefined values:

   ```bash
   helm lint <chart-name>
   ```

   Replace `<chart-name>` with the actual name of your Helm chart.

2. **Check `values.yaml`:**
   Examine the `values.yaml` file in your Helm chart. Unused values may be present if there are keys defined in `values.yaml` that are not referenced anywhere in your chart's templates.

3. **Manual Inspection:**
   Manually inspect your Helm chart's templates (files in the `templates` directory) for references to values. Check if there are values defined in `values.yaml` that are not used in these templates.

4. **Use `grep` or Other Tools:**
   You can use command-line tools like `grep` to search for specific values in your chart files. For example:

   ```bash
   grep -r "some-value" .
   ```

   Replace `"some-value"` with the value you want to search for.

   Additionally, tools like `ack` or IDEs with advanced search functionalities can help you search for specific values or keys across multiple files.

5. **Code Review and Documentation:**
   Review the Helm chart code and documentation. Sometimes, unused values may be commented out or left in the code for future use. A code review and documentation review can help identify such cases.

6. **Consider Using `kubeval`:**
   `kubeval` is a tool that can validate your Kubernetes manifests against the Kubernetes API schemas. While it won't directly identify unused Helm values, it can help ensure that your manifests are valid. Install `kubeval` using:

   ```bash
   brew install kubeval
   ```

   Run it on your rendered templates:

   ```bash
   kubeval --strict --ignore-missing-schemas ./rendered-templates
   ```

   Replace `./rendered-templates` with the directory containing your rendered templates.

Remember that Helm values can be dynamically used in templates, so the absence of a direct reference does not necessarily mean a value is unused. Manual inspection, linting, and a good understanding of your Helm chart are crucial for accurately identifying and handling unused values.




--------------------------

--------------------------
--------------------------

# LINUX :


30. have you come across exit status, why we use that exit status ?

Yes, the exit status is a numeric value that a command or a script returns to the operating system upon completion of execution. It is sometimes referred to as the "exit code" or "return code." The exit status serves several purposes:

1. **Indication of Success or Failure:**
   - An exit status of 0 typically indicates successful execution.
   - A non-zero exit status typically indicates an error or failure.

2. **Communication between Processes:**
   - Other programs or scripts can check the exit status to determine the success or failure of the executed command.
   - This is especially important in scripting or automation, where one command's success might dictate the next steps.

3. **Debugging and Troubleshooting:**
   - When running commands or scripts interactively or as part of a larger system, knowing the exit status helps in identifying and troubleshooting issues.
   - Different exit status codes can provide information about the nature of an error or failure.

4. **Conditional Execution:**
   - In scripts or shell commands, the exit status can be used in conditional statements (`if` statements) to determine the flow of the script based on the success or failure of a command.

For example, in a bash script:

```bash
#!/bin/bash

some_command

if [ $? -eq 0 ]; then
    echo "Command succeeded"
else
    echo "Command failed"
fi
```

Here, `$?` represents the exit status of the last executed command. The script checks if the exit status is 0, indicating success, and takes appropriate action.

It's worth noting that conventionally, an exit status of 0 indicates success, and any other value indicates an error or failure. Different commands or programs may use specific non-zero exit codes to convey different types of errors. The specifics can be found in the documentation of the individual commands or programs.

--------------------------

31. command to find the os of system ?



In Linux, there are various commands you can use to find information about the operating system. Here are several commands you can try:

1. **`lsb_release`:**
   ```bash
   lsb_release -a
   ```
   This command provides detailed information about the Linux distribution, including its name, release number, and codename.

2. **`cat /etc/os-release`:**
   ```bash
   cat /etc/os-release
   ```
   This command displays the contents of the `/etc/os-release` file, which contains information about the operating system, including its name.

3. **`uname`:**
   ```bash
   uname -a
   ```
   This command displays system information, including the kernel version, machine architecture, and the operating system name.

4. **`hostnamectl`:**
   ```bash
   hostnamectl
   ```
   This command provides information about the system and its configuration, including the operating system.

5. **`cat /proc/version`:**
   ```bash
   cat /proc/version
   ```
   This command shows information about the Linux kernel and its version.

Choose the command that best suits your needs or use a combination of them to gather comprehensive information about your Linux system.





-----------
-------------


# ANSIBLE
--------------------------

32. in ansible if we have to run few command on centos and linus how to do that >




--------------------------

33. ansible galaxy ? why we use ?



--------------------------

34. simple example of adhoc command ?




--------------------------

35. how to store the output of command ?




--------------------------




36. what are handlers in ansible and why we use it ?



--------------------------


37. what are the aws services you have worked on ?  
