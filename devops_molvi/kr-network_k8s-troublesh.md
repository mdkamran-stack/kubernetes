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


