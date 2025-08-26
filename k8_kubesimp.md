# day 1 command

docker run -d --name my-nginx-container --memory 512m --cpus 1 nginx  
ps aux | grep '[n]ginx' | sort -n -k 2 | head -n 1 | awk '{print $2}'  
lsns -p pid  
systemd-cgls --no-pager  
cat /sys/fs/cgroup/memory/system.slice/  docker-5ba642ac2146b6d7f2c538d673a480f2ab6a4cec8142eae034286fdefcb5d024.scope/memory.stat  

  ## what is kubectx   

  “kubectx is used to switch between Kubernetes contexts quickly. For example, if I have multiple clusters like dev, staging, and prod, I can just run:

```bash
kubectx dev
kubectx staging
kubectx prod
```

Kubernetes 
=========
kubectl run nginx --image=nginx 

## Day 2

## Create CSR
openssl genrsa -out kamran.key 2048  
openssl req -new -key kamran.key -out kamran.csr -subj "/CN=kamran/O=group1"  

## Sign CSE with Kubernetes CA
cat kamran.csr | base64 | tr -d '\n'

Now we create csr

vi csr.yaml

```bash
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: kamran
spec:
  request: BASE64_CSR
  signerName: kubernetes.io/kube-apiserver-client
  usages:
  - client auth
  ```
  kubectl apply -f csr.yaml kubectl certificate approve saiyam

  kubectl get csr saiyam -o jsonpath='{.status.certificate}' | base64 --decode > saiyam.crt

  ## Role and role binding
```bash
  kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
---
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: read-pods
  namespace: default
subjects:
- kind: User
  name: saiyam
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io  
```
## setup kubeconfig
kubectl config set-credentials saiyam --client-certificate=saiyam.crt --client-key=saiyam.key kubectl config get-contexts kubectl config set-context saiyam-context --cluster=kubernetes --namespace=default --user=saiyam kubectl config use-context saiyam-context

## Merging multiple KubeConfig files
export KUBECONFIG=/path/to/first/config:/path/to/second/config:/path/to/third/config

========================================

Create a file deploy.json
```bash
kubectl create deployment nginx --image=nginx --dry-run=client -o json > deploy.json
kubectl run nginx --image=nginx --dry-run=client -o json
```

## SA creation (Service Account)

```bash
kubectl create serviceaccount sam --namespace default
kubectl create clusterrolebinding sam-clusteradmin-binding --clusterrole=cluster-admin --serviceaccount=default:sam
kubectl create token sam
TOKEN=outputfromabove
APISERVER=$(kubectl config view --minify -o jsonpath='{.clusters[0].cluster.server}')
List deployments
curl -X GET $APISERVER/apis/apps/v1/namespaces/default/deployments -H "Authorization: Bearer $TOKEN" -k
Create Deployment
curl -X POST $APISERVER/apis/apps/v1/namespaces/default/deployments \
  -H "Authorization: Bearer $TOKEN" \
  -H 'Content-Type: application/json' \
  -d @deploy.json \
  -k

List pods 
curl -X GET $APISERVER/api/v1/namespaces/default/pods \
  -H "Authorization: Bearer $TOKEN" \
  -k  
  ```



