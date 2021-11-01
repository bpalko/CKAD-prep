# USEFUL KUBECTL COMMANDS:
https://kubernetes.io/docs/reference/kubectl/cheatsheet/

## POD
kubectl get pods 
kubectl get nodes
kubectl run (name) --image=(image) (creates a pod with a name and a image)
kubectl delete (object) (name) (Can use to delete pod for example)
kubectl run nginx --image=nginx (Spin up a pod quickly)
kubectl run nginx --image=nginx --dry-run=client -o yaml (Spin up pod manifest)

## DEPLOYMENT
Kubectl create -f (file) (will create a file)
Kubectl get replicationcontroller
Kubectl get replicaset
Kubectl replace -f (file) (will update an existing file. Can use this to increase replicas for example)
Kubectl scale --replicas=6 -f (file) (scale replicas without editing file)
Kubectl scale --replicas=6  replicaset (name of replicaset) (this is a direct way to access your replicaset without knowing the filename. It operates off a (type) and a (name)
kubectl create deployment --image=nginx nginx
kubectl create deployment --image=nginx nginx --dry-run -o yaml
kubectl create deployment nginx --image=nginx --replicas=4

## NAMESPACE
Kubectl … --namespace 
Kubectle create -f (file)
Kubectl create namespace (name)
Kubectl config set-context (kubectl config current-context) --namespace=dev (this is like the token commands)
Accessing outside the namespace would be:
(service-name).svc.cluster.local

## SERVICE
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml (Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379)
NOTES ON RUNNING PODS AND DEPLOYMENTS WITH EDIT
Kubectl edit pod (podname) -- this will open the pod spec in an editor. Then edit required props.This will not let you save, but it will save a tmp file that you can then apply after you delete the running pod
Second option is to extract the pod definition in YAML using: 
kubectl get pod webapp -o yaml > my-new-pod.yaml
Open in vim and then save. Delete existing, and redeploy
Deployments are easier with: 
kubectl edit deployment my-deployment
CONFIGMAPS
Kubectl create configmap (config-name) --from-literal=(key)=(value) (IMPERATIVE)
Kubectl create configmap app-config --from-file=app_config.properties (IMPERATIVE)
Kubectl create -f configmap.yaml (DECLARATIVE)
Kubectl get configmaps
Can reference a ConfigMap in three ways:
envFrom>configMapRef>-configmap>name
env>valueFrom>...
Volume mount the file (too much work)


## SECRETS
Kubectl create secret generic (secret-name) --from-literal=(key)=(value)
Kubectl get secrets

## TAINTS AND TOLERATIONS
Kubectl taint nodes node-name key=value:taint-effect
Taint effect can be things like NoSchedule, PreferNoSchedule, NoExecute
Kubectl taint nodes node1 (key)=(value):(effect)
These do not tell pods they cannot do some action, rather it tells the node what can/cannot be mounted
Master nodes automatically get a taint to disallow any mounting (obv apps shouldnt be on the master)
Kubectl describe node (name) | grep Taint
See good google docs https://cloud.google.com/kubernetes-engine/docs/how-to/node-taints

## NODE SELECTOR
Kubectl label nodes (node-name) (label-key)=(label-value)
Kubectl label nodes node-1 size=Large
Spec:
    Containers:
        …
    nodeSelector:
        size:Large

## NODE AFFINITY
Available:
requiredDuringSchedulingIgnoredDuringExecution
preferredDuringSchedulingIgnoredDuringExecution
Planned:
requiredDuringSchedulingRequiredDuringExecution

## NEW CONTENT 9-21
## DOCKER
Docker run -t (tagname) .   (needs to call a directory with a Dockerfile)
Docker images (list all images)
Docker build -p (host port):(exposed port) (image) (p = port)

