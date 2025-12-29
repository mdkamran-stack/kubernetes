pod is unable to schedule   pod is in pending status

## kubectl describe pod , kuebectl get events, kubectl get componentstatus 

kubectl get pod  -n kube-system

scheduler is not started

mv kube-scheduler.yaml /etc/kubernetes/manifest 

kubectl get nodes -l disk=hdd

kubectl label nodes worker-2 disk=hdd

kubectl get nodes -l disk=hdd

kubectl describe node worker |grep -i taint    it is taint in ogs says untolerated

kubectl edit deploy  name 

## spec
    tolerations:
     - key: red
      effect: NoSchedule

kubectl get pod |grep pod name

## to untaint 
kubectl taint node worker red:NoSchedul-

## what is affinity vs antiaffinity in k8s

affinity means scheduling pods together based on rules (e.g., co-locating workloads), while anti-affinity means restrict scheduling pods running them on the same
node or topology.

## Suppose we have schedule a pod on node2 if not available then goes on node3

kubectl label node worker-2 region=india

kubectl label node worker-3 region=india

kubectl label node worker-2 zone=powe1a

kubectl label node worker-3 zone=powe1b

## vi demo.yaml

apiVersion: v1
kind: Pod
metadata:
  name: with-node-affinity
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: region    ## changes
            operator: In
            values:
             - india           ## here changes
      preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 1
        preference:
          matchExpressions:
          - key: zone
            operator: In
            values:
            - powe1a   ## here changes
  containers:
  - name: with-node-affinity
    image: nginx    ## chnaged


## kubectl create -f demo.yaml

kubectl get pod demo.yaml -o wide

## what are the types of probes

Liveness restarts the container, readiness controls traffic, and startup handles slow application initialization.

## diff bw node affinity antiafinity  vs pod affinity antiafinity.

Node affinity controls Pod placement based on node labels, while Pod affinity controls Pod placement relative to other Pods.

## diff b/w node labe selector taint and toleration

Node Label Selector	Pod ↔ Node	Ensures pods are scheduled on nodes with specific labels

Taint	Node ↔ Pod	Marks a node as unsuitable for certain pods unless they tolerate it

Toleration	Pod ↔ Node (response to taint)	Allows pods to ignore taints and be scheduled on tainted nodes  

## what is Image pull policy

there are 3 type of image policy 1> always 2> If not present 3> Never  

Always	The image is pulled from the registry every time the pod starts.  

IfNotPresent	The image is pulled only if it’s not already present on the node.  

Never	The image is never pulled; Kubernetes uses only what’s already on the node.  

## what is diff bw replicaset bw relication controller

A ReplicationController (RC) is the older Kubernetes resource that ensures a specified number of pod replicas are running, while a ReplicaSet (RS) is its more advanced replacement that supports more powerful label selectors and is the default used by Deployments today

## compute quota vs resource quota

Compute Quota limits CPU and memory usage, while Resource Quota limits the overall number and amount of Kubernetes resources within a namespace.

# To check the resources in node 
kubectl describe node | grep -i -A5 'Allocated'

# To check how many nodes3 how many pods are running
kubectl describe node worker-3  

## To check the limit range min to  max we can give for deplymnet 
kubectl describe limit range 

## Horizontal scaling vs vertical scaling  

 Horizontal scaling (scale out) means adding more machines/instances to distribute load.

Vertical scaling (scale up) means upgrading a single machine with more CPU, memory, or storage.

## have to learn pv & pvc make a note

PV is the actual storage resource provided by the cluster, while PVC is the user’s request to claim and use that storage.

## what is label and selector

Labels are key‑value tags on Kubernetes objects, and selectors are queries that filter or match those objects based on their labels.

# One pv will claim in one pvc
# dynamic provisioning suppose we want 1 gb it will provide one 1gb and it is identified by access mode and size .

## what is namespace in k8s
A namespace is used to logically isolate and manage Kubernetes resources within a single cluster.

## what is difference b/w deployment statefulset and Daemonset.

Deployment: webapplication microservices RestAPI
StatefuleSet: Database Message queue distibuted system (Elastic search Kafka)
Daemonset: Logging Agent Fluentd (Prometus node exporter) Network plugins.  

## what is Repicaset
Replicaset Ensures Specified no of pod running all time.

## kubernetes network pod to pod cmmunications 
Any pod can communnicate with any pod or services using their ip address or name, to secure this k8s has provided network policies  

There are 2 types of traffic ingress and Egress  

For Ingress we will specify in from where traffic comes in pod to identify the identity of pod we use pod selector in pod selector we pass label from traffic coming.
select the matchlabels and role and in ports we will specify the port number and protocol.  

case1: suppose we want to provide DB pod form same defaut namespace  - podSelector:  >> matchlabels:  >> role: backend  

case2: suppose our backend pod is not in default namespace it is present in prod namespace the how we will allow 
Then we have to add namepaceSelector: >> matchlabels: >> ns: prod   
It says that those backend pod which is reside in prod namespace can access DB database

case3: in namespace Selector we will add - means we are allowing all pod which is present in prod namespace can access DB pod.  

case4: suppose there is any server which is out of k8s cluster and allow to access db 
In this case we will allow server ip protocol and and its ports   
- ipBlock: cidr: 172.17.9.0/16  >> ports: >> - protocol: TCP  >> port: 6379
In ingress we have used From and for Egress we used to 





