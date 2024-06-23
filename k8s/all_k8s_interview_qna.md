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


Q25 : what is init container and side-car container?can you give simple scenario where we use these conatiners?

- ans :


```
- Init / sidecar enhance functionality of pods
- Init : 
- run b4 main container starts
- performs initialization task setup /conf/ data prep /creating files or dir /
- install dependenncies / wait for ext svc to be available / run health check to know envt is ready 
- perfect for conditions met b4 main app starts
- eg and manifest


- Sidecar :
- additional containers that run alongside of main application in same pod
- enhance functionality of main container without modifying main app code
- logging n monitoring / caching/ load balancing / service discovery / security
```



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



```

- rolling update  : gradually replaces instances of old with new version ( % or N )
- maintains healthy replicas during update
- k8s ueses replica set to ensure specofoc number of replicas running all the time
- when we create deployment it manages the replica set
- when new version updated in deployment configuration k8s create new replica set
- rolling update ... controlled scaling
- readiness and liveness probes
- monitors the state of pod then gradually scales down old version
- auto rollback to to previous version by scaling down new replica set
- minimizes downtime/ test new version of app b4 fully deploying / can conf speed of upate.

```





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


```
- expose applications and manage network communication
- Cluster IP :
--  internal network communication within the cluster,
--  expose servoce on cluster internal ip , only internal service can access 
--  not accessible from outside the cluster

- NodePort :
-- expose service on static port on server ip
-- accessibke from outside of cluster.
-- When traffic is directed to a node's IP and the defined port, the service forwards it to the appropriate pod.

- loadBalancer :
-- exposes service on cloud load balancer
-- distribute external traffic  to pods behind the service
-- suitable for HA and high traffic

- External name :
-- map service to DNS 
-- do not have selector or endpoint but instead redirects DNS queries to specified external name

- Headless : 
-- provides direct DNS based pod to pod communication 

- Ingress :
-- not exactly a service but manages external access to services in your cluster.
-- used to configure rules for routing external traffic to specific service based on HTTP or HTTPS routes
```






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

```
- both are related and work together to ensure communication within the cluster
- Pods :
-- smallest deployable unit , contain 1 or more container , share resources, communicate via localhost

- Services :
-- provide a stable . network internal endpoint to access group pods
-- provides a way to load balance traffic across multiple pods 

- Label selector :
-- pods are labelled with key value pairs & services are configured with label selector to identify pods
-- label selector defines which pods are part of service

- service endpoint :
-- after creating service k8s discovers pods and forms a list of endpoint ,
-- these endpoints are the individual pod ip address and ports that belong to the service
-- service maintains the list and dynamically updates it as pods are reated or terminated

```



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



--------------------------------------------



Kubernetes
--------------------------------------------------------------------------------------------------------------------------------------
33. List objects you know in kubernetes?Give a brief about each object?

ans : 

In Kubernetes, there are several core objects that define the desired state of your applications and infrastructure. Here's a list of common Kubernetes objects along with a brief description of each, and an example manifest file for each:

### 1. **Pod:**
- **Description:** The smallest and simplest Kubernetes object. A Pod represents a running process in a cluster and can contain one or more containers.
- **Manifest Example (pod.yaml):**
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: myapp-pod
  spec:
    containers:
    - name: myapp-container
      image: myapp-image:latest
  ```

### 2. **Service:**
- **Description:** Exposes a set of Pods as a network service. It provides a stable endpoint that can be used to connect to your application.
- **Manifest Example (service.yaml):**
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: myapp-service
  spec:
    selector:
      app: myapp
    ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  ```

### 3. **Deployment:**
- **Description:** Manages the deployment and scaling of a set of Pods. It provides declarative updates to applications.
- **Manifest Example (deployment.yaml):**
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
          image: myapp-image:latest
  ```

### 4. **Ingress:**
- **Description:** Exposes HTTP and HTTPS routes to services. It allows external access to services based on rules.
- **Manifest Example (ingress.yaml):**
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

### 5. **ConfigMap:**
- **Description:** ConfigMaps allow you to decouple configuration artifacts from the container image. They can be used to store configuration data in key-value pairs.
- **Manifest Example (configmap.yaml):**
  ```yaml
  apiVersion: v1
  kind: ConfigMap
  metadata:
    name: myapp-config
  data:
    app_config: |
      key1: value1
      key2: value2
  ```

### 6. **Secret:**
- **Description:** Similar to ConfigMaps, Secrets are used to store sensitive information such as passwords, tokens, or keys.
- **Manifest Example (secret.yaml):**
  ```yaml
  apiVersion: v1
  kind: Secret
  metadata:
    name: myapp-secret
  type: Opaque
  data:
    username: <base64-encoded-username>
    password: <base64-encoded-password>
  ```

### 7. **PersistentVolume (PV) and PersistentVolumeClaim (PVC):**
- **Description:** PVs and PVCs are used for storage management. A PersistentVolume represents a piece of networked storage in the cluster, while a PersistentVolumeClaim is a request for storage by a user.
- **Manifest Examples:**
  - PersistentVolume (pv.yaml):
    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: myapp-pv
    spec:
      capacity:
        storage: 1Gi
      accessModes:
        - ReadWriteOnce
      hostPath:
        path: /data/myapp
    ```
  - PersistentVolumeClaim (pvc.yaml):
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: myapp-pvc
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 1Gi
    ```

### 8. **Namespace:**
- **Description:** Namespaces are a way to divide cluster resources between multiple users, teams, or applications. They provide a scope for names and are intended for use in environments with many users and applications.
- **Manifest Example (namespace.yaml):**
  ```yaml
  apiVersion: v1
  kind: Namespace
  metadata:
    name: myapp-namespace
  ```

### 9. **Job:**
- **Description:** Represents a task that runs to completion. It is suitable for short-lived, batch-style tasks.
- **Manifest Example (job.yaml):**
  ```yaml
  apiVersion: batch/v1
  kind: Job
  metadata:
    name: myapp-job
  spec:
    template:
      metadata:
        name: myapp-job-pod
      spec:
        containers:
        - name: myapp-container
          image: myapp-job-image:latest
    completions: 1
  ```

### 10. **DaemonSet:**
- **Description:** Ensures that a copy of a Pod runs on all or some nodes in the cluster. Useful for deploying monitoring agents, log collectors, etc., on every node.
- **Manifest Example (daemonset.yaml):**
  ```yaml
  apiVersion: apps/v1
  kind: DaemonSet
  metadata:
    name: myapp-daemonset
  spec:
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
          image: myapp-image:latest
  ```

These examples cover a range of Kubernetes objects that you might encounter when managing and deploying applications in a Kubernetes cluster. The choice of which objects to use depends on your application's requirements and the architecture of your deployment.







-------------------------------

34. Command to list pods and deployments

ans :

To list pods and deployments in a Kubernetes cluster, you can use the following commands with the `kubectl` command-line tool:

### List Pods:

```bash
kubectl get pods
```

This command will display a list of all pods in the current namespace.

To list pods in a specific namespace, use:

```bash
kubectl get pods -n <namespace>
```

### List Deployments:

```bash
kubectl get deployments
```

This command will display a list of all deployments in the current namespace.

To list deployments in a specific namespace, use:

```bash
kubectl get deployments -n <namespace>
```

These commands provide a quick overview of the current status of pods and deployments in your Kubernetes cluster. If you need more detailed information, you can use additional options such as `-o wide` or check the specific fields using `-o custom-columns`.


--------------------------------------------




Kubernetes
--------------------------------------------------------------------------------------------------------------------------------------
33. List objects you know in kubernetes?Give a brief about each object?

ans : 

In Kubernetes, there are several core objects that define the desired state of your applications and infrastructure. Here's a list of common Kubernetes objects along with a brief description of each, and an example manifest file for each:

### 1. **Pod:**
- **Description:** The smallest and simplest Kubernetes object. A Pod represents a running process in a cluster and can contain one or more containers.
- **Manifest Example (pod.yaml):**
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: myapp-pod
  spec:
    containers:
    - name: myapp-container
      image: myapp-image:latest
  ```

### 2. **Service:**
- **Description:** Exposes a set of Pods as a network service. It provides a stable endpoint that can be used to connect to your application.
- **Manifest Example (service.yaml):**
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: myapp-service
  spec:
    selector:
      app: myapp
    ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  ```

### 3. **Deployment:**
- **Description:** Manages the deployment and scaling of a set of Pods. It provides declarative updates to applications.
- **Manifest Example (deployment.yaml):**
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
          image: myapp-image:latest
  ```

### 4. **Ingress:**
- **Description:** Exposes HTTP and HTTPS routes to services. It allows external access to services based on rules.
- **Manifest Example (ingress.yaml):**
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

### 5. **ConfigMap:**
- **Description:** ConfigMaps allow you to decouple configuration artifacts from the container image. They can be used to store configuration data in key-value pairs.
- **Manifest Example (configmap.yaml):**
  ```yaml
  apiVersion: v1
  kind: ConfigMap
  metadata:
    name: myapp-config
  data:
    app_config: |
      key1: value1
      key2: value2
  ```

### 6. **Secret:**
- **Description:** Similar to ConfigMaps, Secrets are used to store sensitive information such as passwords, tokens, or keys.
- **Manifest Example (secret.yaml):**
  ```yaml
  apiVersion: v1
  kind: Secret
  metadata:
    name: myapp-secret
  type: Opaque
  data:
    username: <base64-encoded-username>
    password: <base64-encoded-password>
  ```

### 7. **PersistentVolume (PV) and PersistentVolumeClaim (PVC):**
- **Description:** PVs and PVCs are used for storage management. A PersistentVolume represents a piece of networked storage in the cluster, while a PersistentVolumeClaim is a request for storage by a user.
- **Manifest Examples:**
  - PersistentVolume (pv.yaml):
    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: myapp-pv
    spec:
      capacity:
        storage: 1Gi
      accessModes:
        - ReadWriteOnce
      hostPath:
        path: /data/myapp
    ```
  - PersistentVolumeClaim (pvc.yaml):
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: myapp-pvc
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 1Gi
    ```

### 8. **Namespace:**
- **Description:** Namespaces are a way to divide cluster resources between multiple users, teams, or applications. They provide a scope for names and are intended for use in environments with many users and applications.
- **Manifest Example (namespace.yaml):**
  ```yaml
  apiVersion: v1
  kind: Namespace
  metadata:
    name: myapp-namespace
  ```

### 9. **Job:**
- **Description:** Represents a task that runs to completion. It is suitable for short-lived, batch-style tasks.
- **Manifest Example (job.yaml):**
  ```yaml
  apiVersion: batch/v1
  kind: Job
  metadata:
    name: myapp-job
  spec:
    template:
      metadata:
        name: myapp-job-pod
      spec:
        containers:
        - name: myapp-container
          image: myapp-job-image:latest
    completions: 1
  ```

### 10. **DaemonSet:**
- **Description:** Ensures that a copy of a Pod runs on all or some nodes in the cluster. Useful for deploying monitoring agents, log collectors, etc., on every node.
- **Manifest Example (daemonset.yaml):**
  ```yaml
  apiVersion: apps/v1
  kind: DaemonSet
  metadata:
    name: myapp-daemonset
  spec:
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
          image: myapp-image:latest
  ```

These examples cover a range of Kubernetes objects that you might encounter when managing and deploying applications in a Kubernetes cluster. The choice of which objects to use depends on your application's requirements and the architecture of your deployment.







-------------------------------

34. Command to list pods and deployments

ans :

To list pods and deployments in a Kubernetes cluster, you can use the following commands with the `kubectl` command-line tool:

### List Pods:

```bash
kubectl get pods
```

This command will display a list of all pods in the current namespace.

To list pods in a specific namespace, use:

```bash
kubectl get pods -n <namespace>
```

### List Deployments:

```bash
kubectl get deployments
```

This command will display a list of all deployments in the current namespace.

To list deployments in a specific namespace, use:

```bash
kubectl get deployments -n <namespace>
```

These commands provide a quick overview of the current status of pods and deployments in your Kubernetes cluster. If you need more detailed information, you can use additional options such as `-o wide` or check the specific fields using `-o custom-columns`.



---------------------------



Kubernetes
--------------------------------------------------------------------------------------------------------------------------------------
33. List objects you know in kubernetes?Give a brief about each object?

ans : 

In Kubernetes, there are several core objects that define the desired state of your applications and infrastructure. Here's a list of common Kubernetes objects along with a brief description of each, and an example manifest file for each:

### 1. **Pod:**
- **Description:** The smallest and simplest Kubernetes object. A Pod represents a running process in a cluster and can contain one or more containers.
- **Manifest Example (pod.yaml):**
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: myapp-pod
  spec:
    containers:
    - name: myapp-container
      image: myapp-image:latest
  ```

### 2. **Service:**
- **Description:** Exposes a set of Pods as a network service. It provides a stable endpoint that can be used to connect to your application.
- **Manifest Example (service.yaml):**
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: myapp-service
  spec:
    selector:
      app: myapp
    ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  ```

### 3. **Deployment:**
- **Description:** Manages the deployment and scaling of a set of Pods. It provides declarative updates to applications.
- **Manifest Example (deployment.yaml):**
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
          image: myapp-image:latest
  ```

### 4. **Ingress:**
- **Description:** Exposes HTTP and HTTPS routes to services. It allows external access to services based on rules.
- **Manifest Example (ingress.yaml):**
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

### 5. **ConfigMap:**
- **Description:** ConfigMaps allow you to decouple configuration artifacts from the container image. They can be used to store configuration data in key-value pairs.
- **Manifest Example (configmap.yaml):**
  ```yaml
  apiVersion: v1
  kind: ConfigMap
  metadata:
    name: myapp-config
  data:
    app_config: |
      key1: value1
      key2: value2
  ```

### 6. **Secret:**
- **Description:** Similar to ConfigMaps, Secrets are used to store sensitive information such as passwords, tokens, or keys.
- **Manifest Example (secret.yaml):**
  ```yaml
  apiVersion: v1
  kind: Secret
  metadata:
    name: myapp-secret
  type: Opaque
  data:
    username: <base64-encoded-username>
    password: <base64-encoded-password>
  ```

### 7. **PersistentVolume (PV) and PersistentVolumeClaim (PVC):**
- **Description:** PVs and PVCs are used for storage management. A PersistentVolume represents a piece of networked storage in the cluster, while a PersistentVolumeClaim is a request for storage by a user.
- **Manifest Examples:**
  - PersistentVolume (pv.yaml):
    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: myapp-pv
    spec:
      capacity:
        storage: 1Gi
      accessModes:
        - ReadWriteOnce
      hostPath:
        path: /data/myapp
    ```
  - PersistentVolumeClaim (pvc.yaml):
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: myapp-pvc
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 1Gi
    ```

### 8. **Namespace:**
- **Description:** Namespaces are a way to divide cluster resources between multiple users, teams, or applications. They provide a scope for names and are intended for use in environments with many users and applications.
- **Manifest Example (namespace.yaml):**
  ```yaml
  apiVersion: v1
  kind: Namespace
  metadata:
    name: myapp-namespace
  ```

### 9. **Job:**
- **Description:** Represents a task that runs to completion. It is suitable for short-lived, batch-style tasks.
- **Manifest Example (job.yaml):**
  ```yaml
  apiVersion: batch/v1
  kind: Job
  metadata:
    name: myapp-job
  spec:
    template:
      metadata:
        name: myapp-job-pod
      spec:
        containers:
        - name: myapp-container
          image: myapp-job-image:latest
    completions: 1
  ```

### 10. **DaemonSet:**
- **Description:** Ensures that a copy of a Pod runs on all or some nodes in the cluster. Useful for deploying monitoring agents, log collectors, etc., on every node.
- **Manifest Example (daemonset.yaml):**
  ```yaml
  apiVersion: apps/v1
  kind: DaemonSet
  metadata:
    name: myapp-daemonset
  spec:
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
          image: myapp-image:latest
  ```

These examples cover a range of Kubernetes objects that you might encounter when managing and deploying applications in a Kubernetes cluster. The choice of which objects to use depends on your application's requirements and the architecture of your deployment.







-------------------------------

34. Command to list pods and deployments

ans :

To list pods and deployments in a Kubernetes cluster, you can use the following commands with the `kubectl` command-line tool:

### List Pods:

```bash
kubectl get pods
```

This command will display a list of all pods in the current namespace.

To list pods in a specific namespace, use:

```bash
kubectl get pods -n <namespace>
```

### List Deployments:

```bash
kubectl get deployments
```

This command will display a list of all deployments in the current namespace.

To list deployments in a specific namespace, use:

```bash
kubectl get deployments -n <namespace>
```

These commands provide a quick overview of the current status of pods and deployments in your Kubernetes cluster. If you need more detailed information, you can use additional options such as `-o wide` or check the specific fields using `-o custom-columns`.




-----------------------------------------




Kubernetes
--------------------------------------------------------------------------------------------------------------------------------------
33. List objects you know in kubernetes?Give a brief about each object?

ans : 

In Kubernetes, there are several core objects that define the desired state of your applications and infrastructure. Here's a list of common Kubernetes objects along with a brief description of each, and an example manifest file for each:

### 1. **Pod:**
- **Description:** The smallest and simplest Kubernetes object. A Pod represents a running process in a cluster and can contain one or more containers.
- **Manifest Example (pod.yaml):**
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: myapp-pod
  spec:
    containers:
    - name: myapp-container
      image: myapp-image:latest
  ```

### 2. **Service:**
- **Description:** Exposes a set of Pods as a network service. It provides a stable endpoint that can be used to connect to your application.
- **Manifest Example (service.yaml):**
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: myapp-service
  spec:
    selector:
      app: myapp
    ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  ```

### 3. **Deployment:**
- **Description:** Manages the deployment and scaling of a set of Pods. It provides declarative updates to applications.
- **Manifest Example (deployment.yaml):**
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
          image: myapp-image:latest
  ```

### 4. **Ingress:**
- **Description:** Exposes HTTP and HTTPS routes to services. It allows external access to services based on rules.
- **Manifest Example (ingress.yaml):**
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

### 5. **ConfigMap:**
- **Description:** ConfigMaps allow you to decouple configuration artifacts from the container image. They can be used to store configuration data in key-value pairs.
- **Manifest Example (configmap.yaml):**
  ```yaml
  apiVersion: v1
  kind: ConfigMap
  metadata:
    name: myapp-config
  data:
    app_config: |
      key1: value1
      key2: value2
  ```

### 6. **Secret:**
- **Description:** Similar to ConfigMaps, Secrets are used to store sensitive information such as passwords, tokens, or keys.
- **Manifest Example (secret.yaml):**
  ```yaml
  apiVersion: v1
  kind: Secret
  metadata:
    name: myapp-secret
  type: Opaque
  data:
    username: <base64-encoded-username>
    password: <base64-encoded-password>
  ```

### 7. **PersistentVolume (PV) and PersistentVolumeClaim (PVC):**
- **Description:** PVs and PVCs are used for storage management. A PersistentVolume represents a piece of networked storage in the cluster, while a PersistentVolumeClaim is a request for storage by a user.
- **Manifest Examples:**
  - PersistentVolume (pv.yaml):
    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: myapp-pv
    spec:
      capacity:
        storage: 1Gi
      accessModes:
        - ReadWriteOnce
      hostPath:
        path: /data/myapp
    ```
  - PersistentVolumeClaim (pvc.yaml):
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: myapp-pvc
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 1Gi
    ```

### 8. **Namespace:**
- **Description:** Namespaces are a way to divide cluster resources between multiple users, teams, or applications. They provide a scope for names and are intended for use in environments with many users and applications.
- **Manifest Example (namespace.yaml):**
  ```yaml
  apiVersion: v1
  kind: Namespace
  metadata:
    name: myapp-namespace
  ```

### 9. **Job:**
- **Description:** Represents a task that runs to completion. It is suitable for short-lived, batch-style tasks.
- **Manifest Example (job.yaml):**
  ```yaml
  apiVersion: batch/v1
  kind: Job
  metadata:
    name: myapp-job
  spec:
    template:
      metadata:
        name: myapp-job-pod
      spec:
        containers:
        - name: myapp-container
          image: myapp-job-image:latest
    completions: 1
  ```

### 10. **DaemonSet:**
- **Description:** Ensures that a copy of a Pod runs on all or some nodes in the cluster. Useful for deploying monitoring agents, log collectors, etc., on every node.
- **Manifest Example (daemonset.yaml):**
  ```yaml
  apiVersion: apps/v1
  kind: DaemonSet
  metadata:
    name: myapp-daemonset
  spec:
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
          image: myapp-image:latest
  ```

These examples cover a range of Kubernetes objects that you might encounter when managing and deploying applications in a Kubernetes cluster. The choice of which objects to use depends on your application's requirements and the architecture of your deployment.







-------------------------------

34. Command to list pods and deployments

ans :

To list pods and deployments in a Kubernetes cluster, you can use the following commands with the `kubectl` command-line tool:

### List Pods:

```bash
kubectl get pods
```

This command will display a list of all pods in the current namespace.

To list pods in a specific namespace, use:

```bash
kubectl get pods -n <namespace>
```

### List Deployments:

```bash
kubectl get deployments
```

This command will display a list of all deployments in the current namespace.

To list deployments in a specific namespace, use:

```bash
kubectl get deployments -n <namespace>
```

These commands provide a quick overview of the current status of pods and deployments in your Kubernetes cluster. If you need more detailed information, you can use additional options such as `-o wide` or check the specific fields using `-o custom-columns`.



----------------------------




Kubernetes
--------------------------------------------------------------------------------------------------------------------------------------
33. List objects you know in kubernetes?Give a brief about each object?

ans : 

In Kubernetes, there are several core objects that define the desired state of your applications and infrastructure. Here's a list of common Kubernetes objects along with a brief description of each, and an example manifest file for each:

### 1. **Pod:**
- **Description:** The smallest and simplest Kubernetes object. A Pod represents a running process in a cluster and can contain one or more containers.
- **Manifest Example (pod.yaml):**
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: myapp-pod
  spec:
    containers:
    - name: myapp-container
      image: myapp-image:latest
  ```

### 2. **Service:**
- **Description:** Exposes a set of Pods as a network service. It provides a stable endpoint that can be used to connect to your application.
- **Manifest Example (service.yaml):**
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: myapp-service
  spec:
    selector:
      app: myapp
    ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  ```

### 3. **Deployment:**
- **Description:** Manages the deployment and scaling of a set of Pods. It provides declarative updates to applications.
- **Manifest Example (deployment.yaml):**
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
          image: myapp-image:latest
  ```

### 4. **Ingress:**
- **Description:** Exposes HTTP and HTTPS routes to services. It allows external access to services based on rules.
- **Manifest Example (ingress.yaml):**
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

### 5. **ConfigMap:**
- **Description:** ConfigMaps allow you to decouple configuration artifacts from the container image. They can be used to store configuration data in key-value pairs.
- **Manifest Example (configmap.yaml):**
  ```yaml
  apiVersion: v1
  kind: ConfigMap
  metadata:
    name: myapp-config
  data:
    app_config: |
      key1: value1
      key2: value2
  ```

### 6. **Secret:**
- **Description:** Similar to ConfigMaps, Secrets are used to store sensitive information such as passwords, tokens, or keys.
- **Manifest Example (secret.yaml):**
  ```yaml
  apiVersion: v1
  kind: Secret
  metadata:
    name: myapp-secret
  type: Opaque
  data:
    username: <base64-encoded-username>
    password: <base64-encoded-password>
  ```

### 7. **PersistentVolume (PV) and PersistentVolumeClaim (PVC):**
- **Description:** PVs and PVCs are used for storage management. A PersistentVolume represents a piece of networked storage in the cluster, while a PersistentVolumeClaim is a request for storage by a user.
- **Manifest Examples:**
  - PersistentVolume (pv.yaml):
    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: myapp-pv
    spec:
      capacity:
        storage: 1Gi
      accessModes:
        - ReadWriteOnce
      hostPath:
        path: /data/myapp
    ```
  - PersistentVolumeClaim (pvc.yaml):
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: myapp-pvc
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 1Gi
    ```

### 8. **Namespace:**
- **Description:** Namespaces are a way to divide cluster resources between multiple users, teams, or applications. They provide a scope for names and are intended for use in environments with many users and applications.
- **Manifest Example (namespace.yaml):**
  ```yaml
  apiVersion: v1
  kind: Namespace
  metadata:
    name: myapp-namespace
  ```

### 9. **Job:**
- **Description:** Represents a task that runs to completion. It is suitable for short-lived, batch-style tasks.
- **Manifest Example (job.yaml):**
  ```yaml
  apiVersion: batch/v1
  kind: Job
  metadata:
    name: myapp-job
  spec:
    template:
      metadata:
        name: myapp-job-pod
      spec:
        containers:
        - name: myapp-container
          image: myapp-job-image:latest
    completions: 1
  ```

### 10. **DaemonSet:**
- **Description:** Ensures that a copy of a Pod runs on all or some nodes in the cluster. Useful for deploying monitoring agents, log collectors, etc., on every node.
- **Manifest Example (daemonset.yaml):**
  ```yaml
  apiVersion: apps/v1
  kind: DaemonSet
  metadata:
    name: myapp-daemonset
  spec:
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
          image: myapp-image:latest
  ```

These examples cover a range of Kubernetes objects that you might encounter when managing and deploying applications in a Kubernetes cluster. The choice of which objects to use depends on your application's requirements and the architecture of your deployment.







-------------------------------

34. Command to list pods and deployments

ans :

To list pods and deployments in a Kubernetes cluster, you can use the following commands with the `kubectl` command-line tool:

### List Pods:

```bash
kubectl get pods
```

This command will display a list of all pods in the current namespace.

To list pods in a specific namespace, use:

```bash
kubectl get pods -n <namespace>
```

### List Deployments:

```bash
kubectl get deployments
```

This command will display a list of all deployments in the current namespace.

To list deployments in a specific namespace, use:

```bash
kubectl get deployments -n <namespace>
```

These commands provide a quick overview of the current status of pods and deployments in your Kubernetes cluster. If you need more detailed information, you can use additional options such as `-o wide` or check the specific fields using `-o custom-columns`.



---------------------------------------------------------------------

https://raw.githubusercontent.com/qriz1452/interview/main/YT/i.%20%20kubernetes%20interview%20-%2002%20%7C%20kubrenetes%20interview%20questions%20%7C%20kubernetes%20telephonic%20interview.md



---------------------------------------------------------------------------


https://github.com/qriz1452/interview/blob/main/YT/j.%20%20kubernetes%20mock%20interview%20-3.md


-------------------------------------------

https://github.com/qriz1452/interview/blob/main/YT/l.%20%20kubernetes%20interview%20(%20kubernetes%20mock%20interview%20).md

