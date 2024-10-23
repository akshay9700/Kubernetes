# kubernetes
Kubernetes files and notes repo <br/>

### K8s Architecture:

![Kubernetes-Architecture](https://github.com/akshay9700/Kubernetes/assets/110522215/9247c00b-adcc-4b32-9f0e-8c97d1f1b3bd)

---

### General Structure of Kubernetes realtime folder
```
my-k8s-project/
│
├── manifests/
│   ├── deployments/
│   │   ├── app-deployment.yaml
│   │   └── other-app-deployment.yaml
│   ├── services/
│   │   ├── app-service.yaml
│   │   └── other-app-service.yaml
│   ├── configmaps/
│   │   └── app-configmap.yaml
│   ├── secrets/
│   │   └── app-secret.yaml
│   ├── persistent-volumes/
│   │   └── app-pv.yaml
│   └── namespaces/
│       └── app-namespace.yaml
│
├── scripts/
│   └── deploy.sh
│
├── charts/
│   └── my-app-chart/
│       ├── templates/
│       │   ├── deployment.yaml
│       │   ├── service.yaml
│       │   └── configmap.yaml
│       └── values.yaml
│
├── README.md
└── k8s-setup.sh
```

GitHub repos: [k8s-repo](https://github.com/antonputra/tutorials/tree/main/lessons/171)


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

```


---

Key Concepts in Kubernetes:
1. Cluster
A Kubernetes cluster is a set of machines (nodes) that run containerized applications. It consists of a control plane (master) and worker nodes.

Control Plane: Manages the state of the cluster, including scheduling applications, maintaining their desired state, scaling, and responding to failures.
Worker Nodes: Run the containerized applications. Each node has its own CPU, memory, storage, and networking resources.

2. Node
A node is a worker machine in Kubernetes, either a physical or virtual machine, where containers run.

Master Node: Runs the Kubernetes control plane processes (API server, scheduler, etcd, etc.).
Worker Node: Runs the application containers and contains components like the kubelet (communicates with the control plane) and kube-proxy (manages network communication).


3. Pod
A pod is the smallest and most basic unit of deployment in Kubernetes. A pod encapsulates one or more containers that are tightly coupled and share the same network namespace and storage.

Single Container Pod: The most common type, running one container.
Multi-Container Pod: Multiple containers that need to run together, often sharing resources like data or communicating over localhost.

4. ReplicaSet
A ReplicaSet ensures that a specified number of pod replicas are running at all times. If a pod crashes or fails, the ReplicaSet automatically replaces it with a new pod.

Purpose: Ensure the high availability and scaling of pods.
Controller: Part of the Kubernetes control loop to ensure the desired number of replicas.

5. Deployment
A Deployment is a higher-level abstraction that manages ReplicaSets and provides declarative updates to pods and ReplicaSets. It allows you to define how many replicas of an application should run, and it handles rolling updates and rollbacks automatically.

Rolling Updates: Incrementally replaces old pods with new ones to ensure no downtime.
Rollback: Reverts to a previous version of the application if something goes wrong.

6. Service
A Service is an abstraction that defines a logical set of pods and a policy for accessing them. Kubernetes Services enable communication between pods, and between pods and external systems.

ClusterIP: The default type, which exposes the service on an internal IP within the cluster.
NodePort: Exposes the service on each node’s IP at a static port.
LoadBalancer: Creates an external load balancer to expose the service to the internet.
ExternalName: Maps a service to an external DNS name.

7. ConfigMap
A ConfigMap is used to store configuration data in key-value pairs that can be injected into containers as environment variables or configuration files. It decouples environment-specific configurations from the application code.

8. Secret
A Secret stores sensitive information, such as passwords, OAuth tokens, and SSH keys. Kubernetes secrets are similar to ConfigMaps but are intended to hold sensitive data.

Base64 encoded: The secret values are stored in Base64 format for safety in transit, though it is not encrypted by default.

9. Volume
A Volume in Kubernetes is a directory that a container can use to store and retrieve data. Kubernetes volumes persist even if the container crashes, unlike container file systems, which are ephemeral.

Types: emptyDir, hostPath, PersistentVolume (PV), PersistentVolumeClaim (PVC), etc.

10. PersistentVolume (PV)
A PersistentVolume is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes. It provides a way to store data outside of the pod's lifecycle.

11. PersistentVolumeClaim (PVC)
A PersistentVolumeClaim is a request for storage by a user. It binds to a PersistentVolume (PV) that meets the requested resources (size, access mode, etc.).

12. Namespace
A Namespace is a way to divide a single Kubernetes cluster into multiple virtual clusters. They help to organize and manage resources and policies across different groups or environments (e.g., dev, test, prod).

Use Case: Useful in large environments with many users working on different projects.


13. Ingress
An Ingress manages external access to services within a Kubernetes cluster, typically HTTP or HTTPS routes. It allows you to configure load balancing, SSL termination, and name-based virtual hosting.

Ingress Controller: A specific implementation that processes ingress rules and configures a load balancer accordingly (e.g., NGINX, Traefik).

14. DaemonSet
A DaemonSet ensures that a copy of a pod runs on all (or some) nodes in the cluster. It is typically used for background tasks, such as log collectors, monitoring agents, or networking daemons.

15. StatefulSet
A StatefulSet is a controller that manages stateful applications. Unlike Deployments, StatefulSets are used for applications that require unique, persistent identities and stable, persistent storage, such as databases.

Persistent Storage: Pods in a StatefulSet have stable network identifiers and persistent storage across restarts.

16. Job and CronJob
Job: A Kubernetes Job creates one or more pods and ensures that a specified number of them successfully terminate. It is used for tasks that should run to completion (e.g., batch processing).
CronJob: A CronJob is a specialized Job that runs on a schedule, similar to a cron task in Unix/Linux.

17. Horizontal Pod Autoscaler (HPA)
The Horizontal Pod Autoscaler automatically adjusts the number of pod replicas in a deployment, replication controller, or statefulset based on observed CPU utilization or other custom metrics.

18. Kubelet
The Kubelet is an agent that runs on each worker node in the cluster. It ensures that containers are running in the pod, monitors their health, and communicates with the Kubernetes API server.

19. Kube-proxy
Kube-proxy is a network proxy that runs on each node in the cluster. It maintains network rules that allow pods to communicate with each other, and external clients to reach services.

20. Etcd
Etcd is the key-value store used by Kubernetes to store all cluster data, including configurations, network details, and state of the pods. It serves as the cluster's source of truth.

