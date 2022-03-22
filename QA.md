# 1. How to create new POD with the nginx image 

1) kubectl run nginx --image=nginx
2) create file like pod-file.yml
    run command: 
    kubectl create -f ./pod-file.yml

# 2. How find what is the used image of the pod?
1) kubects describe pods
2) kubectl describe pod "pod-name"
3) kubectl describe pod "pod-name" | grep -i image

# 3. What nodes are this pods placed on?
   1) kubectl get pod -o wide 
   2) run: kubectl describe pod "pod-name"
   and look for field "Node"

# 4. How to delete pod
kubectl delete pod "pod-name"

# 5. How to create simple manifest file template?

kubectl run redis --image=redisNewImage --dry-run=client -o yaml > redis-definition.yaml

# 6. How edit and update EXISTING pod 
kubectl edit pod 'pod-name'

# 7.How to extract a pod definition to a file
kubectl get pod "pod-name" -o yaml > pod-definition.yaml




kubectl apply -f pod-file.yaml 