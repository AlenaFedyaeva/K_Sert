# K_Sert

# CNCF Certification
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

