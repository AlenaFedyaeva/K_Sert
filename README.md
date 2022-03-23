# Usefull links

https://kubernetes.io/docs/reference/kubectl/overview/

https://kubernetes.io/docs/reference/kubectl/cheatsheet/

Certified Kubernetes Application Developer: https://www.cncf.io/certification/ckad/

Candidate Handbook: https://www.cncf.io/certification/candidate-handbook

Exam Tips: https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad


# Commands

1) create pod
``` 
kubectl create -f pod-definition.yml
```
2) see information
``` kubectl get pods

kubectl describe pod nyapp-pod
```

3) create replication controller
```
kubectl create -f repl-controller-definition.yml
```

4) replication controller listed
```
kubectl get replicationcontroller 
```
5) create replica set
```
kubectl create -f replicaset-definition.yml
```
6) list replicaset
```
kubectl get replicaset
```
## Ways to scale replicaset

7) update number of replicas in definition, then run:
```
kubectl replace -f replicaset-definition.yml
```

8) run scale command, specify definition file
```
kubectl scale --replicas=6 -f replicaset-definition.yml
```

9) run scale command, specify replicaset name
**W: need to add "rs/" before replicaset name, for command to work**

```
kubectl scale --replicas=6 rs/myapp-replicaset
```

10) delete replicaset
**This also delete ALL underlying PODs**
```
kubectl delete replicaset myapp-replicaset
```

11) create deployment
```
kubectl create -f deployment-definition.yml
kubectl get deployments
```

12) **show all**
```
kubectl get all
```
## HELP inside kubectl
13) View explain 
```
kubectl explain deployment 
```

## Replication controller & Replica Set
Replication controller is the older technology that is beeing replaces by Replica Set. They very similar. They:   
  1) helps run multiple instances
  2) automaticly bring up pod when it failed
  3) help scale application
  4) balance the load across multiple pods on differenet node

But have some differences 

1) Replica set can manage pods that were created before replica set by using their labels. 
2) Definition file for Replica set has field SELECTOR

Selector is the major difference between Replica set and replication controller


## Deployment

Deployment automaticly create ReplicaSet. ReplicaSet automaticly create Pods. 
**Defference between deployment and replicaset: Deployment creates a new Kubernates object - deployments**


## Namespace
By default all pods create in Default namespace.

### 1) Get from default namespace
```
kubectl get pods
```
This command return only pods that been placed in Default namespace.
### 2) Get pods from other namespace

```
kubectl get pods --namespace=<your-namespace>
```

### 3) Create pod in your namespace use
```
kubectl create -f pod.yml --namespace=<your-namespace>
```

Or you can move namespace definition in pod.yml file 

### 4) Create Namespace
create file.yml
```
apiVersion: v1
kind: Namespace
metadata: 
  name: dev
```

and run 

```
kubectl create -f file.yml
//or just  
kubectl create namespace <namespace-name>

```



## Resource Quota

create file with limits request.yml:
```
apiVersion: v1
kind: ResoursesQuota
metadata:
  name: compute-quota
  namespace: dev
spec:
  hard: "10"
  requests.cpu: "4"
  requests.memory: 5Gi
  limits.cpu: "10"
  limits.memory: 10Gi
```

```
kubectl createa -f request.yml
```
