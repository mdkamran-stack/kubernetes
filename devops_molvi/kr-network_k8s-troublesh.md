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

affinity means scheduling pods together based on rules (e.g., co-locating workloads), while anti-affinity means scheduling pods to avoid running them on the same
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

## diff bw node affinity antiafinity  vs pod affinity antiafinity.

Node Affinity / Anti-Affinity controls which nodes a Pod can or cannot be scheduled on using node labels, whereas Pod Affinity / Anti-Affinity controls where Pods are placed relative to other Pods using Pod labels

There are multiple application we always keep close Eg: Redis service should run with web service otherwise it will create latency Suppose redis service goes on node1
and web service goes on node2 These 2 service we always couple in same node. here we have to write pod affinity rule b/w redis and web-service. 
Antiaffinity means redis 2 pod couldnt run on same node should be stopped by pod anti affinity.
If we want to maintance distnace then antiafinity come in picture , of we want to couple then affinity come in picture.

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

