# Kubernetes  (k8s)
K8s is opensouce 
k8s is a captain it watches all the conatainers it watches all the application running inside those container weather it is healty or it is crashing every responsibilities owned by k8s.

## inshort: K8s is a container orchestration platform capable of running different worloads in different environments with great fexibility.  

## container orchestration 

Automate   
 . Provisioning  
 . Scaling   
 . Deploying   
 . Deleting  

2 Used for scale up and scale down.

3 Loadbalancing >> pod1 pod2 pod3  LB eualally distibute the traffic among multiple pods on the same N/W  

Feature : Self Healing  if any pod fail it will detect and recreate also detect worker nodes 

it is used for Rollouts & Rollbacks 

Rollout automatically rollout our changes if its not per our expectation we can rollback those changes.

## What is K8s Used for.  

1 K8s used for container orchestration  
2 Self Healing   
3 scaling application  
4 Loadbalancing  
5 Networking  
6 Automatically rolling out and rolling back changes using yaml .  


## k8s architectur  
1. Kube-API is responsible for authentication & auth to create delete and manage worker nodes.  
2. Kube scheduler its communicate with API server to schedule pods on worker nodes  
3. Kube controller manager maintain & monitor clsuter  current states.  
4. Etcd contain whole data of cluster.  

## Worker Node 3 component :  
1. kubeletet: 
2. Kube-proxy:
3. container run time:  

## What is K8s Cluster.  

1. A K8s cluster is a group of nodes that run containerized Applications.  
2. A k8s cluster is a group of one or more nodes with running pods.  
3. K8s cluster allow application to be developed, moved and managed.  
4. Container can run across multiple machines and environments, including virutal, physical, cloud-based, and on-premises.
5. K8s cluster are comprised of one mater node and a no.of worker nodes.  

## What is master-node  
1. A master node in k8s manages the cluseter.  
2. It also known as the Control Plane.  
3. The master node is reponsible for cluster mgmt & for providing the API that is used to configure and manahe resources within the k8s cluster.  
4. It is also responsible for mgmt of worker nodes.  
5. The Control Plane or the Master Node acts as the brain of the k8s cluster.  
6. The k8s cluster typically has 3 master nodes.  
7. Three dedicated master nodes, the recommended number, provides two backup nodes in the event of a master node failure & the necessary quorun (2) to elect a new master.

## What is worker Node?
1. A worker node in k8s is a machine that runs containerized app and handles networking for a cluster.  
2. worker nodes run app process data and handle networking.  
3. k8s runs our workload by placing container into pods on the worker nodes.  
4. The main responsibilities of a worker node is proces data stored in the cluster & handle n/w to ensures traffic b/w the application across the cluster & outside of the cluster properly facilited.
5. we can have one worker node in 1 k8s cluster as the minimum number.  

## What is K8s Cluster.  
A set of nodes managed by k8s, A cluster consist of master and worker nodes A nodes is a linux server.  

## What is Node:
A Node in k8s is a physical or virtual M/C that provides the computing power to run workloads. if a node fails, its automatically removed from the cluster & other nodes take over.  

## What is Pod:
It is smallest unit of execution in the k8s system. it is made up of one or more conatiners. A pod is a collection of containers that work together to server a common purpose.

## what is Namespace:
A Namespace is an isolated environment in a cluster. The resources belonging to different namespaces cant directly interact with one another.  

## What is Deployment:
A deployment manages a set of pods to run an application workload. The Deployment is a way to automate the process of creating and managing multiple replicas of the application, making it easier to manage, update, and scale our application without worrying about the underlying infrastructure.

## Service:
A Service groups pods and exposes them for external traffic as a single entity in k8s services are commony used to expose pods to external or internal traffic.

## Replicaset:
A group of identical pods running for a specific workloads is a Replicaset. A replicaset purpose is to keep a specified no of identical pods running at all times.This helps to ensure that an application is availabe and reliable even if some parts of it fail.  

## ConfigMap:
A configMap is a type of native API objects designed to store environment-specific 
configuration data and share it with pods A configMap is k8s object used to store non-confidetial data in key-value pairs. 
Config-map can be created using kubectl commands or YAML files.  

## Ingress:
Ingress means how external users access the applications or services. k8s ingress is the mechanism used to present services and application externally from within a cluster it can be a website , a blog that is accessed on a web browser.  

## DaemonSet:
A Deamonset ensures that all (or some) Nodes run a copy of a pod, As nodes are added to the cluster, pods are added to them. Daemonset is k8s feature taht lets you run a k8s pod on all cluster nodes taht meet certain criteria. node is removed from the cluster the pod is removed when a daemonset is deleted k8s removes all the pods created by it.

## NodePort
A nodeport is a k8s service that allows external clients to access applications by opening a port on every node in a cluster , This service Opens a port on every node in a cluster , and forward traffic to the service.

## PortRange: Typically 30000-32767 , but customizable

In Short Nodeport are a basic way to expose services to external traffic.

## Secrets:
In k8s, a Secret is an object that stores sensitive information, such as password,Oauth tokens, and SSH Keys.

## RBAC
Role-Based Access Control is securtiy feature in k8s that controls access to resources based on that roles of users and service accounts. RBAC defines permissions that specify what users and service account can do with resources , such as creating, updating, and deleting.
RBAC helps secure your environment and reduce the risk of unauthorized access.  

## Annotation: just like a label.
Since we know label attaches metadata to the k8s objects, Annotations simply considered as the advanced form of labels with more features. Annotations can conatin more charachter that labels and can be structured or Unstructured.  

## Cluster IP
In k8s a cluster ip is a fixed internal ip address that used to facilitate communication within a cluster.  
ClusterIp assigns an IP address from a reserved pool to a pod or replica , it defines one or more ports to listen on, and uses target ports to forward TCP/UDP traffic to conatiner.

## LoadBalancer:
Distributes the request across multiple nodes within a cluster.  

## StatfeulSet
A StatefulSet is a set of pods with a unique, persistent hostname and ID. Statefulset are designed to run stateful application in k8s with dedicated persistent storage.  
When pods run as part of Statefulset, k8s keeps state data in the persistent storage volumes of the statefulset of the statefulset even pods shutdown.  

# Kubernetes Terms

## Clsuter >> set of nodes 
## Node >> A linux server
## Pod >> collection of container
## Namespace >> The isolated workspace for resources.
## Deployment >> Create & Modify Pods  
## Service >> Multipe pods acting as a single resource.
## ReplicaSet >> Stable set of pods  
## DaemonSet >> Runs copy of pods on each node.
## Statfulset >> Manages a group of pods  
## ConfigMap >> stores non-sensitive data.
## Ingress >> External Access to the Services.
## Secrets >> A password or token
## NodePort >> Allows external accessibility of apps.
## RBAC >> Users and service account permissions.
## Annotation >> To label objects.
## ClusterIP >> Cluster's internal IP address 
## LoadBalancer >> Equal traffic distribution

## Running few kubectl commands
kubectl cluster-info

kubectl config view

kubectl get nodes

kubectl get pods

kubectl get pods  --all-namespaces 

## Deploy NGINX web server on Minikube and access locally
kubectl create deployment devops-web --image=nginx:latest

kubectl get deployment

kubectl expose deployment devops-web --port=80 --type=LoadBalancer

kubectl get services

kubectl get pods

## cluster information in more granular way.

kubectl clsuter-info dump  

## Get the information about node in details.

kubectl describe node nodename (in my case conrtolplan)  

## overview of all the resources in cluster

kubectl get all  

kubectl option (for more deeper)  

## Api related info (when we have to the verison upgradations)

kubectl api-resources  

kubectl api-version (supprted api & version)  

## To get the namespace (A namespace in Kubernetes is a logical partition within a cluster that allows you to organize and isolate resources. It’s mainly used for multi-tenancy, environment separation (like dev, test, prod),)

kubectl get namespaces  

kubectl config set-context --current --namespace=dev  (to create ns)  

kubectl config set-context --current --namespace=controlplane  

kubectl get pods  

kubectl create namespace mytestns  

kubectl get namespaces  

kubectl delete namespace nameofns  (verydanger cmd be concious)  

kubectl get pods -n kube-system  

kubectl get pods --all-namespaces ( to list of very namespace)  

kubectl get pods -o wide --all-namespaces  

kubectl get pods -A  (same as above cmd)  

## To check specific pods logs details 

kubectl describe pod pod-name -n  namespace  
kubectl describe pod es-cluster-0 -n kamran

kubectl get pods -A  

kubectl logs name -n Namespace  

kubectl logs -f name -n Namsapce ( like tail cmd)  

## To login any pods 

kubectl get pods  

kubectl exec -it Name of pod -- /bin/bash  (now we are mving inside the pod)  

kubcetl run pod2 --image=alpine:latest ( to create new pod)  

kubctl get pods   

## For deployment 

kubectl get deployment   

kubectl create deployment deployment-name --image=nginx:latest  

kubectl get deployments --all-namespaces (to list down all namespaces of deployment in our k8s )  

kubectl delete deployment deployment name   

## To list services of namespaces  

kubectl get sevice --all-namespaces  

kubectl delete service Nameof service  

kubectl create service loadbalancer nameof service --tcp=80:8080  (80 is internal port 8080 is external port)  

## configmap dela with non-sensituve data 

kubectl get configmaps -n default  

kubectl describe configmap Name -n kube-system  

## To get the secrets of any k8s clsuter 

kubectl get secrets --all-namespaces  

## FOr statefulsets

kubectl get statefulsets --all-namespaces  

## Replicaset , identical no.of pod in replicaset.

kubectl get replicaset --all-namespaces  

kubectl get daemonset --all-namespaces

## To monitor a nodes & pods

kubectl top nodes  

kubectl top pods  

## for live status of pods

kubectl get pods --watch --all-namespaces  

## To get whole cluster configurations

`kubectl  config view`  

`kubectl config view` ==> To view your current Kubernetes configurations.

`kubectl exec -it es-cluster-0 -- /bin/bash` ==> Connect with elasticsearch-0 pod using SSH.

## pv & pvc pv is something attached to a pod & pvc is per vol claim for attached to pod, we have to claim once succeful then it will attached to pod.

## diff b/w Replicaset vs Daemonset vs Statefulset.

Replicaset ensures that identical no.of pod running at every time if i am using 3 replica means 3 pods are always running on my worker nodes.

Daemonset: It ensure 1 pod is running on each worker node best for log collection monitoring and security agents.

Statefulset: application which need persistent data stores each pod will get dedicated persistent volume attached to it for data storage if we have application using mysql or mongodb.

## Roles RBAC 
Roles is set of permission for specific namespace.
Cluster Roles set of permissions for Entire clsuter.







































 









