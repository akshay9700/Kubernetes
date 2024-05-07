# kubernetes
Different Kubernetes files are present in this repo <br/>

NodePort range is 30000 to 32767

## kubectl imp commands 

```
kubectl get pods                                          
kubectl get nodes                                          
kubectl get pods -o wide                                          
kubectl describe pod <podname>                                          
kubectl logs <podname>                                          
kubectl exec -it <podname> /bin/bash                                          
kubectl get pods -n <namespacename>                                          
kubectl delete --all all                                          
kubectl apply -f <filename>                                          
kubectl get svc                                          
kubectl edit svc <svcname>                                   #
kubectl scale deployment <deploymentname> --replicas 3
kubectl get all
kubectl top nodes                                          
kubectl top pods                                          
kubectl get hpa -w                                           # to display events for every 15sec 
kubectl get events
kubectl
```

RBAC(Role Based Access Controller)  


**K8s Architecture:**
![Kubernetes-Architecture](https://github.com/akshay9700/Kubernetes/assets/110522215/9247c00b-adcc-4b32-9f0e-8c97d1f1b3bd)

