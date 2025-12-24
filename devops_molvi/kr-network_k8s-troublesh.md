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

affinity means scheduling pods together based on rules (e.g., co-locating workloads), while anti-affinity means scheduling pods apart to avoid running them on the same
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
