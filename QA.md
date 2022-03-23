## Pod
### 1. How to create new POD with the nginx image? 

1) run particular image in a pod
```
kubectl run nginx --image=nginx
```
2) create from file 'pod-file.yml' : 
```
kubectl create -f ./pod-file.yml
```
3) create if not exist (or apply if configuration exist)
```
kubectl apply -f pod-file.yaml 
```
### 2. How find what is the used image of the pod?
1) 
``` 
kubects describe pods
```
2) 
```
kubectl describe pod "pod-name"
```
3)
```
kubectl describe pod "pod-name" | grep -i image
```

### 3. What nodes are this pods placed on?
   1) 
   ```
   kubectl get pod -o wide 
   ```
   2) run:
   ```
    kubectl describe pod "pod-name"
   ```
   and look for field "Node"

### 4. How to delete pod?
```
kubectl delete pod "pod-name"
```
### 5. How to create simple manifest file template?
```
kubectl run redis --image=redisNewImage --dry-run=client -o yaml > redis-definition.yaml
```
### 6. How edit and update EXISTING pod? 
```
kubectl edit pod 'pod-name'
```
### 7.How to extract a pod definition to a file?
```
kubectl get pod "pod-name" -o yaml > pod-definition.yaml
```
## ReplicaSet

### 1. How to update replicaset 

1) Edit replicaset with cmd (runs VIM editor)

``` 
kubectl edit replicaset new-replica-set
```
modify and then save the file. 
2) Delete the previous pods to get the new ones with the correct image. 
 ```
 kubectl delete pod 'pod-name' 
 ```


## Deployment 

### 1) How to find deployment image?

Need to find deployment name, then run cmd describe and find field "image"

```
kubectl get deployment
kubectl describe deployment 'name-deployment'

```


### 2) How to find reason why deployment not ready yet? 

Need to run cmd and look under the Events section.
```
kubectl describe pods <pod-name>
```

### 3) How to create deployment from templates with image and scale it?

```
kubectl create deployment <deployment-name> --image=httpd.2.4-alpine
kubectl scale deployment --replicas=3 <deployment-name>
```


## Namespace 

### 1) How to replace default namespace with another one?

```
kubectl config set-context $(kubectl config current-content) --namespace=<your-namespace>
```
 
 ### 2) How to list all pods from all namespaces?

```
kubectl get pods --all-namespaces
```

## ResourceQuota
to specify resources


#
What DNS name should the Blue application use to access the database 'db-service' in the 'dev' namespace

You can try it in the web application UI. Use port 6379.

Since the blue application and the db-service are in different namespaces in this case, we need to use the service name along with the namespace to access the database. The FQDN (fully Qualified Domain Name) for the db-service in this example would be db-service.dev.svc.cluster.local.

Note: You can also access it using the service name and namespace like this: db-service.dev



