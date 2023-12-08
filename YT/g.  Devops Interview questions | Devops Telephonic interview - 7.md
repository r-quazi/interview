##  Devops Interview questions | Devops Telephonic interview - 7 
https://www.youtube.com/watch?v=ndhcVCJ21IQ&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=7

------------------------------------------------------------



GIT

1. Branching strategy you followed in production ?

Ans : 
The branching strategy you follow in a production environment can vary depending on your team's workflow, the complexity of your project, and your specific needs. However, a common branching strategy that many teams adopt is called "GitFlow." GitFlow defines a set of branching and merging rules to manage feature development, bug fixes, and releases effectively. Here's a high-level overview of the GitFlow branching strategy:

1. **Main Branches:**

   - **Master**: The `master` branch represents the production-ready code. It should always contain the latest stable release of your software.
   
   - **Develop**: The `develop` branch is where active development takes place. It's a branch where all feature development and bug fixes are merged before being released to production. It should be relatively stable but can have unfinished features.

2. **Supporting Branches:**

   - **Feature Branches**: Feature branches are created for developing new features or enhancements. They branch off from the `develop` branch and are merged back into `develop` when the feature is complete.

   Example:
   ```bash
   git checkout develop
   git checkout -b feature/new-feature
   # Work on the new feature
   git commit -m "Add new feature"
   git checkout develop
   git merge feature/new-feature
   ```

   - **Release Branches**: When you're ready to prepare a new release, you create a `release` branch from the `develop` branch. This branch is used for final testing, bug fixes, and preparing the release. Once the release is ready, it's merged into both `master` and `develop`.

   Example:
   ```bash
   git checkout develop
   git checkout -b release/1.0
   # Perform testing and bug fixes
   git checkout master
   git merge release/1.0
   git tag 1.0
   git checkout develop
   git merge release/1.0
   ```

   - **Hotfix Branches**: Hotfix branches are created to address critical issues in the production code. They branch off from `master`, and after the fix is complete, they are merged into both `master` and `develop`.

   Example:
   ```bash
   git checkout master
   git checkout -b hotfix/1.0.1
   # Fix the critical issue
   git commit -m "Fix critical issue"
   git checkout master
   git merge hotfix/1.0.1
   git tag 1.0.1
   git checkout develop
   git merge hotfix/1.0.1
   ```

3. **Version Tagging:**

   For each release and hotfix, you create version tags. This makes it easy to reference specific points in your project's history.

   Example:
   ```bash
   git tag 1.0     # Tagging a release
   git tag 1.0.1   # Tagging a hotfix
   ```

This GitFlow branching strategy helps maintain a structured and organized workflow, ensuring that the `master` branch always contains production-ready code, while development, testing, and bug fixing are done in separate branches. It's important to note that while GitFlow is a well-established strategy, you can adapt it to suit your team's specific needs and preferences.


-----------
------------

2. github api and use cases and how you used in your projects ?
Ans :

GitHub provides a powerful API (Application Programming Interface) that allows developers to interact programmatically with their repositories, issues, pull requests, users, and more. The GitHub API can be used in various ways and has a wide range of use cases. Here are some common use cases for the GitHub API and how it can be utilized in projects:

1. **Automated Testing and Continuous Integration (CI/CD)**:
   - You can use the GitHub API to trigger automated tests and CI/CD pipelines whenever changes are pushed to a repository. Services like Travis CI, CircleCI, and GitHub Actions integrate with the API to automatically build, test, and deploy code.

2. **Issue and Bug Tracking**:
   - GitHub API allows you to create, update, and close issues programmatically. You can integrate it with your bug tracking system or use it to manage project tasks and user stories.

3. **Pull Request Automation**:
   - You can automate various aspects of your pull request workflow using the GitHub API. For example, you can automatically label, assign, or comment on pull requests based on certain criteria.

4. **Repository Management**:
   - You can use the API to create, delete, or manage repositories. This is useful for automated repository creation or archival.

5. **User Management**:
   - You can manage users and their access to repositories using the API. For example, you can add collaborators or remove access programmatically.

6. **Data Analysis and Reporting**:
   - GitHub API provides access to a wealth of data about repositories, issues, and users. You can use this data to generate reports, track trends, or perform analytics on your projects.

7. **Integration with External Services**:
   - You can integrate GitHub with other external services, such as chat applications (Slack, Microsoft Teams), project management tools (Trello, Asana), or code review platforms (Code Climate, SonarQube).

8. **Custom GitHub Bots**:
   - You can create custom GitHub bots that perform actions based on specific events or conditions. For example, you can build a bot that automatically thanks contributors or enforces coding standards.

9. **Documentation Generation**:
   - GitHub API can be used to trigger documentation generation processes whenever changes are made to code repositories. This ensures that documentation is always up-to-date.

10. **Security Scanning and Dependency Management**:
    - You can use the API to integrate security scanning tools and dependency management services into your workflow. This helps identify and mitigate security vulnerabilities in your codebase.

In my projects, I've used the GitHub API for various purposes:

- **Continuous Integration**: I've set up CI/CD pipelines that are triggered by GitHub webhooks and interact with the API to build and deploy applications automatically.

- **Issue Tracking**: I've developed custom scripts that create GitHub issues based on bug reports received from users through other channels.

- **Release Automation**: I've automated the process of creating GitHub releases and tagging them with the API as part of the CI/CD pipeline.

- **Custom Notifications**: I've built GitHub bots that monitor repositories for specific events (e.g., new pull requests) and send notifications to team members through Slack or email.

- **User Access Management**: I've used the API to manage user access to repositories, adding or removing collaborators as needed.

The GitHub API is versatile and can be tailored to meet the specific needs of your project, whether it's enhancing your development workflow, automating tasks, or integrating with other tools and services.

----------------------------
OR

I apologize for the confusion. Let's break down each use case into step-by-step technical instructions:

**1. Automated Testing and CI/CD:**

   a. Set up GitHub Actions:
      - In your GitHub repository, navigate to the "Actions" tab.
      - Click on "New workflow" or create a new workflow file in the `.github/workflows` directory.

   b. Define a workflow file (e.g., `.github/workflows/main.yml`) with triggers:
      ```yaml
      name: CI/CD Pipeline
      on:
        push:
          branches:
            - main
      ```

   c. Specify jobs and steps in the workflow to build, test, and deploy your application.
   
   d. Use GitHub Actions environment variables (e.g., `GITHUB_TOKEN`) to authenticate with the GitHub API in your workflow.

**2. Issue and Bug Tracking:**

   a. Generate a personal access token:
      - Go to your GitHub account's "Settings."
      - Under "Developer settings," select "Personal access tokens."
      - Generate a token with "repo" or more specific scopes.

   b. In your application code, use a library like Octokit (for JavaScript) or PyGitHub (for Python) to authenticate with the GitHub API using the personal access token.

   c. Use the library to create, update, close, or query issues as needed.

**3. Pull Request Automation:**

   a. Create a webhook:
      - In your GitHub repository, navigate to "Settings" > "Webhooks."
      - Add a new webhook, specifying the payload URL of your server or application.

   b. Develop a server or application that listens to GitHub webhook events, especially `pull_request` events.

   c. Use the GitHub API to interact with pull requests programmatically (e.g., add labels, assignees, or comments) based on your desired automation logic.

**4. Repository Management:**

   a. Authenticate your application with a personal access token or OAuth token that has repository management permissions.

   b. Use the GitHub API to create, delete, or modify repositories as needed.

**5. User Management:**

   a. Authenticate your application with a personal access token or OAuth token that has user management permissions.

   b. Use the GitHub API to invite collaborators, modify user roles, or remove access as required.

**6. Data Analysis and Reporting:**

   a. Authenticate your application with a personal access token or OAuth token.

   b. Use the GitHub API to fetch data (e.g., repository statistics, issue/pull request details).

   c. Process the retrieved data in your preferred programming language or data analysis tool.

**7. Integration with External Services:**

   a. Set up a webhook in your GitHub repository to send events to an endpoint in your external service.

   b. In your external service, develop handlers that receive and process GitHub events using the GitHub API.

**8. Custom GitHub Bots:**

   a. Create a GitHub bot account if you don't already have one.

   b. Develop a bot application that uses a GitHub API library to listen for specific GitHub events.

   c. Implement custom actions or behaviors based on these events using the GitHub API.

**9. Documentation Generation:**

   a. Set up a webhook in your GitHub repository to trigger documentation generation when code changes occur.

   b. Develop a documentation generation script or tool that uses the GitHub API to clone the repository, generate documentation, and commit/push changes back to the repository.

**10. Security Scanning and Dependency Management:**

    a. Integrate security scanning and dependency management tools into your CI/CD pipeline.

    b. Use the GitHub API within your CI/CD scripts to trigger scans and checks on your codebase.

    c. Review and act upon the results generated by these tools within your CI/CD workflow.

Please note that these are general steps, and the specific implementation details may vary based on your programming language, tools, and infrastructure choices. Additionally, always follow best practices for security and authentication when working with the GitHub API.





----------
-----------

3. how you will list the the branches using the API ?


To list branches using the GitHub API, you can make a GET request to the `branches` endpoint of a specific repository. Here are the step-by-step instructions:

1. **Authentication**:
   - Before making any requests to the GitHub API, you need to authenticate. You can use a personal access token or OAuth token for this purpose.

2. **Make a GET Request**:
   - Use your preferred programming language and HTTP library or a GitHub API client library (e.g., Octokit for JavaScript, PyGitHub for Python) to make a GET request to the `branches` endpoint of the repository.

   - The API endpoint URL for listing branches follows this format:
     ```
     https://api.github.com/repos/:owner/:repo/branches
     ```

   - Replace `:owner` with the owner (user or organization) of the repository and `:repo` with the name of the repository.

   - Example using cURL (replace placeholders with actual values):
     ```bash
     curl -H "Authorization: token YOUR_ACCESS_TOKEN" \
          https://api.github.com/repos/OWNER/REPO/branches
     ```

   - Example using Python and the `requests` library:
     ```python
     import requests

     # Replace with your access token and repository details
     access_token = "YOUR_ACCESS_TOKEN"
     owner = "OWNER"
     repo = "REPO"

     headers = {
         "Authorization": f"token {access_token}"
     }

     url = f"https://api.github.com/repos/{owner}/{repo}/branches"

     response = requests.get(url, headers=headers)
     if response.status_code == 200:
         branches = response.json()
         for branch in branches:
             print(branch["name"])
     else:
         print(f"Failed to fetch branches: {response.status_code}")
     ```

3. **Process the Response**:
   - The response from the API will be in JSON format and contain information about each branch in the repository.
   - You can parse the JSON response and extract the branch names or any other branch-related information you need for further processing.

This will give you a list of branches in the specified repository. You can then use this information for various purposes, such as automation, reporting, or managing branches within your project.

--------
----------


4. what is webhook and where you used webhooks ?

A webhook is a mechanism for one system or application to send real-time data or event notifications to another system or application. Webhooks allow systems to communicate with each other by sending HTTP POST requests to a predefined URL (endpoint) when specific events or triggers occur. The receiving system or application can then take action based on the data received.

Webhooks are commonly used for various purposes, including:

1. **Automation**: Webhooks are used to trigger automated actions or workflows in response to specific events. For example, you can use webhooks to trigger build and deployment processes when code is pushed to a repository.

2. **Integration**: Webhooks enable the integration of different services or systems. For instance, you can use webhooks to send notifications from one application to another, such as posting updates to a chat platform when certain events happen in a project management tool.

3. **Real-time Data**: Webhooks provide a way to receive real-time data updates. They are commonly used in applications like messaging apps, social media platforms, and news feeds to notify users of new messages, posts, or updates.

4. **Monitoring and Logging**: Webhooks can be used to monitor and log events in a system. For instance, you can set up webhooks to log user sign-ins, error occurrences, or changes to critical data.

5. **Alerting**: Webhooks are often used for alerting and notification purposes. When critical events occur, such as server outages or security breaches, webhooks can send alerts to relevant personnel or systems.

6. **Data Synchronization**: Webhooks can help keep data synchronized between systems. For example, an e-commerce platform may use webhooks to update inventory levels in real-time across multiple sales channels.

7. **Custom Automation**: Developers can create custom webhooks to implement specific actions or integrations tailored to their application's needs.

As for where webhooks are used, they are employed in a wide range of applications and services across different industries. Some common use cases for webhooks include:

- **GitHub Webhooks**: GitHub uses webhooks to notify external systems or services about various events in repositories, such as code pushes, pull requests, and issue updates. This allows for the automation of CI/CD pipelines, issue tracking, and more.

- **Slack Incoming Webhooks**: Slack provides incoming webhooks that allow users to post messages and updates to Slack channels from external sources and applications. This is commonly used for integration with other tools and services.

- **Payment Gateways**: Payment processors often use webhooks to notify merchants about payment events, such as successful transactions, refunds, and chargebacks.

- **Chat Applications**: Many chat applications, like Discord and Microsoft Teams, support webhooks that can be used to send messages, alerts, or updates to chat channels.

- **IoT Devices**: Internet of Things (IoT) devices can use webhooks to send data or trigger actions when specific conditions are met, such as temperature thresholds or sensor readings.

Webhooks provide a flexible and efficient way to enable real-time communication and automation between different systems and services, making them a valuable tool in modern software development and system integration.






----------
----------

5. where the configurations like username and email are stored in git ? file name ? 

In Git, the configurations for the username and email address associated with commits are typically stored in the local repository configuration files. The specific configuration settings are stored in a file named `.gitconfig`, which is located either at the repository level or at the global user level. Here's an explanation of both:

1. **Repository-level Configuration**:
   - The repository-level configuration is stored in a file named `.git/config` within the root directory of the Git repository.
   - This configuration file stores settings that are specific to the current repository, and they take precedence over global settings.
   - To set the username and email address for a specific repository, you can use the following Git commands within the repository directory:
     ```bash
     git config user.name "Your Name"
     git config user.email "your.email@example.com"
     ```
   - These settings will be saved in the `.git/config` file for that repository.

2. **Global-level Configuration**:
   - The global-level configuration is stored in a file named `.gitconfig` or `.config/git/config` in the user's home directory.
   - This configuration file stores settings that apply to the user across all Git repositories on the system.
   - To set the global username and email address that will be used by default for all repositories, you can use the following Git commands in the command line:
     ```bash
     git config --global user.name "Your Name"
     git config --global user.email "your.email@example.com"
     ```
   - These settings will be saved in the user's global `.gitconfig` file.

It's important to note that while the repository-level configuration allows you to set username and email address specific to a particular project, the global-level configuration is used as a fallback when repository-specific values are not set. This means that if you don't set username and email at the repository level, Git will use the global values.

You can view the current Git configuration for a repository or globally by running the following commands:

- To view the repository-level configuration:
  ```bash
  git config --local --list
  ```

- To view the global-level configuration:
  ```bash
  git config --global --list
  ```

These commands will display all the configuration settings, including username and email, stored in the respective configuration files.


or in credential manager.


---------------------------------------


## k8s :

--------------------------------------------

Q. what is k8s objects and ingress and what service have you used in k8s deployment ? 

Ans : 
In Kubernetes (often abbreviated as K8s), objects are the fundamental entities used to represent and manage the state of your application or system. These objects are defined in YAML files and submitted to the Kubernetes API server, which then takes care of deploying and managing the specified resources. Some common Kubernetes objects include:

1. **Pods:** The smallest deployable units in Kubernetes, representing a single instance of a running process.

2. **Services:** Abstractions that define a set of Pods and how they can be accessed. Services enable network access to a set of Pods, either within the cluster or from external sources.

3. **ReplicaSets:** Controllers that ensure a specified number of replicas (identical copies) of Pods are running at all times.

4. **Deployments:** Higher-level abstractions that manage ReplicaSets and provide declarative updates to applications.

5. **ConfigMaps and Secrets:** Objects for storing configuration data and sensitive information, respectively, separately from the Pod's specification.

6. **Ingress:** An API object that manages external access to services within a cluster, typically HTTP. Ingress allows you to define how external traffic should be directed to your services.

Speaking specifically about Ingress:

- **Ingress:** In Kubernetes, Ingress is an API object that provides HTTP and HTTPS routing to services based on rules. It acts as a layer of abstraction for external access to services and allows you to define how external traffic should be directed to your services. Ingress controllers are responsible for implementing the rules set in the Ingress resource.

Regarding services used in Kubernetes deployments, it depends on the specific requirements of the application. Commonly used services include:

- **ClusterIP Service:** Exposes the service on a cluster-internal IP. It's accessible only within the cluster.

- **NodePort Service:** Exposes the service on each Node's IP at a static port. It allows external traffic to reach the service.

- **LoadBalancer Service:** Exposes the service externally using a cloud provider's load balancer. It automatically assigns an external IP and routes traffic to the service.

- **ExternalName Service:** Maps the service to the contents of the `externalName` field (e.g., a DNS name).

- **Headless Service:** Acts as a service discovery mechanism without load balancing. Each Pod gets its own DNS entry.

The choice of service type depends on factors such as the application architecture, traffic requirements, and the underlying infrastructure.


-------------------------------------------------------

Q. How do you deploya feature with zero downtime in k8s ?
Ans:

Deploying a feature with zero downtime in Kubernetes involves careful planning and execution. Here are some strategies and best practices to achieve zero-downtime deployments:

1. **ReplicaSets and Deployments:**
   - Use ReplicaSets or Deployments to manage your Pods. These controllers ensure that a specified number of replicas are running at all times.
   - Deployments, in particular, allow you to perform rolling updates by gradually replacing old Pods with new ones.

2. **Rolling Updates:**
   - Leverage rolling updates provided by Deployments. This strategy replaces instances of the old application with the new one gradually, minimizing downtime.
   - The default behavior for Deployments is a rolling update.

3. **Readiness Probes:**
   - Implement readiness probes in your Pods. Readiness probes define conditions under which a Pod is considered ready to serve traffic.
   - During a deployment, Kubernetes checks the readiness status of each Pod. If a Pod is not ready, it is not included in the load balancing, ensuring traffic only goes to healthy Pods.

4. **Liveness Probes:**
   - Use liveness probes to determine if a Pod is still running. If a Pod fails its liveness probe, Kubernetes will restart it or stop routing traffic to it.
   - This helps in identifying and recovering from situations where the application is running but not functioning correctly.

5. **Rolling Restart:**
   - Perform rolling restarts for your application when configuration changes are needed. This involves updating one or a few Pods at a time, ensuring that the application remains available.

6. **Blue-Green Deployments:**
   - Set up a blue-green deployment strategy where you have two sets of identical environments (blue and green).
   - Deploy the new feature to the "green" environment while the "blue" environment is still serving traffic.
   - Once the green environment is validated, switch traffic to it, making it the new live environment.

7. **Canary Deployments:**
   - Gradually roll out the new feature to a subset of users or traffic using canary deployments.
   - Monitor the canary release for issues, and if everything is stable, gradually increase the traffic to the new version.

8. **External Load Balancer Health Checks:**
   - If you're using an external load balancer, configure health checks to ensure it only directs traffic to healthy Pods.

9. **Persistent Storage Considerations:**
   - If your application uses persistent storage, ensure that changes in the new version are backward-compatible with the data format of the previous version.

10. **Monitoring and Rollback:**
    - Implement monitoring and alerting to detect issues early. If problems are detected, be prepared to rollback the deployment to the previous version.

By following these practices, you can significantly reduce or eliminate downtime during feature deployments in Kubernetes. Always test these strategies in a staging environment before applying them to a production environment.












------------------------------------------------------------

Q. what you used before  introducing replica set ?
Ans:

Before the introduction of ReplicaSets in Kubernetes, the primary mechanism for managing sets of identical Pods was through a simpler controller called Replication Controllers. Replication Controllers served a similar purpose but lacked some of the advanced features and flexibility provided by ReplicaSets and Deployments, which are now more commonly used.

Here's a brief overview of Replication Controllers and why ReplicaSets were introduced:

1. **Replication Controllers:**
   - Replication Controllers were the earlier controller in Kubernetes for managing and ensuring the desired number of replicas of Pods.
   - They were responsible for maintaining a specified number of identical Pods running at all times.
   - Replication Controllers had limitations, such as the inability to perform rolling updates with fine-grained control over the update process.

2. **Introduction of ReplicaSets:**
   - ReplicaSets were introduced to address some shortcomings of Replication Controllers and to provide more flexibility in managing Pod replicas.
   - ReplicaSets have selector-based matching for identifying the Pods they manage, making them more expressive and powerful.
   - They introduced the concept of rolling updates, allowing for controlled and automated updates of Pods.

3. **Key Differences:**
   - While both ReplicaSets and Replication Controllers can be used for basic replication, ReplicaSets offer more expressive selector options for identifying Pods.
   - ReplicaSets also enable more sophisticated update strategies, such as rolling updates, which allow for gradual replacement of old Pods with new ones.
   - Deployments, a higher-level abstraction built on top of ReplicaSets, provide additional features for declarative updates, rollbacks, and more.

In summary, ReplicaSets replaced Replication Controllers as the preferred way to manage replicated Pods in Kubernetes due to their improved features and capabilities. Deployments, which use ReplicaSets under the hood, are commonly used for managing application lifecycle events, including rolling updates, scaling, and rollbacks, providing a more powerful and user-friendly experience.








----------------------------------------------------

Q. what is exact difference between replicaset and replica controllers ? 
Ans:

ReplicaSet and Replication Controller are both Kubernetes controllers designed to ensure a specified number of identical Pod replicas are running. However, there are some key differences between the two:

1. **Selector Options:**
   - ReplicaSet allows more expressive and powerful selector options for identifying the Pods it manages. It supports the full set of equality-based selectors as well as set-based selectors.
   - Replication Controller only supports equality-based selectors.

2. **Selector Matching:**
   - ReplicaSet supports set-based matching, allowing you to use conditions like "in," "not in," "exists," and "does not exist" for selector matching.
   - Replication Controller supports only equality-based matching for selectors.

3. **Update Strategies:**
   - ReplicaSet introduces more advanced update strategies, especially the ability to perform rolling updates. Rolling updates allow for controlled replacement of old Pods with new ones, ensuring a smooth transition during application updates.
   - Replication Controller has a basic rolling update strategy, but it lacks some of the fine-grained control provided by ReplicaSets.

4. **Pod Template Changes:**
   - When using ReplicaSet, if you update the Pod template (e.g., changing the container image), it triggers a rolling update to ensure the desired state is achieved gradually.
   - With Replication Controller, updating the Pod template directly may not trigger a controlled rolling update, potentially causing abrupt changes to the entire set of Pods.

5. **API Version:**
   - ReplicaSet is part of the "apps" API group in Kubernetes, and its API version is `apps/v1`.
   - Replication Controller is part of the "core" API group, and its API version is `v1`.

In practical terms, ReplicaSets are considered more powerful and flexible compared to Replication Controllers. They provide enhanced selector options, support for set-based matching, and improved update strategies. Deployments, a higher-level abstraction built on ReplicaSets, are commonly used for managing application lifecycle events due to their additional features, including declarative updates, rollbacks, and more sophisticated deployment strategies.












---------------------------------------------



Q. As soon as you deploy a new deployemnt how replicaset and rolling update works ? 
Ans:

When you deploy a new Deployment in Kubernetes, the following process occurs, involving ReplicaSets and rolling updates:

1. **Desired State Declaration:**
   - You define the desired state of your application in a Deployment manifest, specifying details such as the container image, number of replicas, and other configuration parameters.
   - The Deployment controller takes this desired state and attempts to make it a reality in the cluster.

2. **ReplicaSet Creation:**
   - The Deployment controller creates a ReplicaSet to manage the specified number of replicas (Pods) based on the desired state.
   - The ReplicaSet is responsible for ensuring that the actual state of the cluster matches the desired state.

3. **Pod Creation:**
   - The ReplicaSet creates the required number of Pods based on the template specified in the Deployment manifest.
   - These Pods are initially created to match the desired state.

4. **Rolling Update Initialization:**
   - If the Deployment manifest is updated (e.g., a new container image is specified), the Deployment controller initiates a rolling update.

5. **New ReplicaSet Creation:**
   - A new ReplicaSet is created with the updated Pod template. This new ReplicaSet represents the desired state after the update.

6. **Scaling Up the New ReplicaSet:**
   - The Deployment controller starts creating new Pods controlled by the new ReplicaSet. The number of new Pods gradually increases while the number of old Pods decreases.

7. **Rolling Replacement:**
   - The rolling update mechanism ensures that the old and new Pods coexist during the process, allowing for a smooth transition without downtime.
   - The Deployment controller monitors the health of the Pods and ensures that the desired number of replicas is maintained throughout the update.

8. **Scaling Down the Old ReplicaSet:**
   - As the new Pods become ready and are confirmed to be healthy, the Deployment controller scales down the old ReplicaSet by terminating Pods controlled by it.

9. **Completion of Update:**
   - The rolling update continues until all old Pods are replaced by new Pods, and the new ReplicaSet fully represents the desired state.
   - The update is considered complete when the Deployment controller determines that the actual state matches the desired state.

10. **Rollback (Optional):**
    - If any issues are detected during the rolling update, Kubernetes allows for automatic or manual rollback to the previous state using the revision history kept by the Deployment controller.

This process ensures that the application is updated with minimal downtime and without disrupting the availability of the service. The rolling update strategy is a key feature of Deployments in Kubernetes, allowing for seamless updates and rollbacks of applications.



















----------------------------------------

## shell scripting :
Q. 
