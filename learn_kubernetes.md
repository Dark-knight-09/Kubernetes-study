## kubernetes
kubernetes is a container orchestration tool that helps in managing containerized applications in different environments.is an open-source platform developed by google, which automates the deployment, scaling, and management of containerized applications.

# Kubernetes Architecture
Kubernetes architecture consists of a master node and a worker node. 
- The master node is responsible for managing the worker nodes and scheduling pods running on them. 
- The worker nodes are responsible for running the containers or pods.

# Master Node
The master node consists of the following components:
- API Server:is the front-end of the control plane. exposes the kubernetes API, which is used by the clients to interact with the cluster.
- Controller Manager:is responsible for running the controller processes, which are responsible for maintaining the desired state of the cluster.
- Scheduler:is responsible for scheduling the pods on the worker nodes based on the resource requirements and constraints.
- etcd:is a distributed key-value store that stores the cluster state. 

# Worker Node
The worker node consists of the following components:
- Kubelet:is responsible for managing containers running on the node and communication between worker node and master node.
- Kube Proxy:is responsible for routing traffic to the pods from outside the cluster (basically internet).
- Container Runtime: Runtime used to run the containers.(DOCKER or containerd)
- Pod:is the smallest unit of deployment in kubernetes.consists of one or more containers that share the same network and storage. (running containers)


## NOTE: 
In Kubernetes, resources are identified by their kind and metadata.name fields. This means that the configuration can be in any file, and as long as the kind and metadata.name match an existing resource, that resource will be updated. If the kind and metadata.name do not match any existing resource, a new resource will be created.

# K8 Commands
kubectl:is a command-line tool used to interact with the kubernetes cluster. 

types of resources in k8s:
1. Pods : smallest unit of deployment in k8s
2. ReplicaSets : ensures specific number of pods are running in cluster
3. Deployments : manages ReplicaSets and Pods
4. Services : provides networking to the pods
5. Nodes : physical or virtual machines in the cluster
6. Namespaces : used to group and isolate resources
7. ConfigMaps : used to store configuration data
8. Secrets : used to store sensitive information
9. Ingress : manages external access to services
10. Volumes : used to persist data in k8s
11. StatefulSets : used to run stateful applications
12. DaemonSets : ensures that all nodes run a copy of a pod
13. Jobs : runs a pod to completion
14. CronJobs : runs a job on a schedule
15. PersistentVolumes : is a piece of storage in the cluster    
16. PersistentVolumeClaims : is a request for storage by a user
17. StorageClasses : is used to dynamically provision persistent volumes
18. HorizontalPodAutoscaler : automatically scales the number of pods in a deployment
19. NetworkPolicy : is used to control the traffic flow between pods



commands:

- kubectl api-resources: displays the resources in the cluster.
- kubectl version:displays the client and server version of kubectl.
- kubectl help:displays the help information for kubectl.
- kubectl get <resource_type> <resource_name>:displays the resources in the cluster.
- kubectl config view:displays the kubectl configuration.

- kubectl create:creates a resource in the cluster.
- kubectl apply:applies the configuration to the cluster.
- kubectl edit:edits the configuration of a resource.
- kubectl delete <resource_type> <resource_name>:deletes a resource from the cluster.
- kubectl describe <resource_type> <resource_name>:displays detailed information about a resource.
- kubectl logs:displays the logs of a container in a pod.
- kubectl exec:executes a command in a container in a pod.
- kubectl run:creates a new pod or deployment.
- kubectl expose:exposes a deployment as a service.
- kubectl scale:scales a deployment.


- kubectl get nodes: displays the nodes in the cluster. (less information)
- kubectl get nodes -o wide: displays the nodes in the cluster with additional information.
- kubectl get pods: displays the pods in the cluster.
- kubectl get services:displays the services in the cluster.
- kubectl get deployments:  displays the deployments in the cluster.
- kubectl get replicasets:  displays the replica sets in the cluster.

# config commands:
- kubectl config view:displays the kubectl configuration.
- kubectl config use-context <context_name>:switches the context in the kubectl configuration.
- kubectl config set-context <context_name>:sets the context in the kubectl configuration.
- kubectl config current-context:displays the current context in the kubectl configuration.
- kubectl config get-contexts:displays the contexts in the kubectl configuration.
- kubectl config delete-context <context_name>:deletes a context from the kubectl configuration.
- kubectl config set-cluster <cluster_name>:sets the cluster in the kubectl configuration.


1. pods: smallest unit of deployment in k8s.consists of one or more containers that share the same network and storage.
- kubectl create pod <pod-name> --image=<image-name>: creates a pod with the specified image.
- kubectl create pod -f <filename>: creates a pod from a file.
- kubectl describe pod <pod-name>: displays detailed information about a pod.
- kubectl exec -it <pod-name> -- /bin/bash: executes a command in a pod.
- kubectl logs <pod-name>: displays the logs of a pod.

2. ReplicaSets: is collection of same pods (number of pods pre-defined in a file), ensures that a specific number of pod are running in the cluster.
- kubectl get rs: displays the replica sets in the cluster.
- kubectl describe rs <replicaset-name>: displays detailed information about a replica set.

3. Deployments: provide features for updates or rollbacks in ReplicaSets and Pods.Deployment is a higher level of abstraction than ReplicaSet.
- kubectl get deployments: displays the deployments in the cluster.
- kubectl create  deployment -f <filename>:creates a deployment from a file.
- kubectl edit deployment <deployment-name>:edits the deployment configuration.
- kubectl apply -f <filename>:applies the configuration from a file.
- kubectl expose deployment <deployment-name> --port=<port>:exposes a deployment as a service on the specified port.
- kubectl create deployment <deployment-name> --image=<image-name>:creates a deployment with the specified image.

# Note: multiple deployments can be created in a single file using '---' separator.
example: 
            ''' apiVersion: apps/v1
            kind: Deployment
            metadata:
                name: deployment1
            spec:
                # specification for deployment1
            ---
            apiVersion: apps/v1
            kind: Deployment
            metadata:
                name: deployment2
            spec:
                # specification for deployment2 '''


4. Services: provides networking to the pods in the cluster. types of network services:
- ClusterIP: exposes the service on a cluster-internal IP.
- NodePort: exposes the service on each node's IP at a static port.
- LoadBalancer: exposes the service externally using a cloud provider's load balancer.
- ExternalName: maps the service to the contents of the externalName field.

- kubectl port-forward <pod-name> <local-port>:<pod-port>: forwards the traffic from a local port to a pod port.
- kubectl expose deployment <deployment-name> --port=<port>: exposes a deployment as a service on the specified port.


> each pod has a unique IP address, and all containers in the pod share the same network namespace, including the IP address and network ports. communication between two pods is done using the pod IP address.
> services provide a stable IP address and DNS name for a set of pods, and they can load balance traffic between the pods. but to connect to a perticular pod, we need to use the pod IP address(not-prefered) or headless service (prefered).
> nodeport service is used to expose the service on each node's IP at a static port (not-prefered). each nodeport service creates a clusterip service to route the traffic to the pods. the static port is in the range of 30000-32767.
> loadbalancer service is used to expose the service externally securely (prefered). it creates a nodeport and a clusterip service.
> clusterip exposes the port on cluster level and nodeport exposes the port on node level and loadbalancer exposes the node port securely.

5. Secrets: are used to store sensitive information like passwords, tokens, and keys. secrets are stored in etcd in base64 encoded format.
- kubectl create secret generic <secret-name> --from-literal=<key>=<value>: creates a secret from a literal value.
- kubectl apply -f <filename>: applies the configuration from a file.
example:
'''
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
    username: "base64encodedusername" 
    password: "base64encodedpassword" 
'''

6. ConfigMaps: are used to store configuration data in key-value pairs. configmaps are stored in etcd in plain text format.
- kubectl create configmap <configmap-name> --from-literal=<key>=<value>: creates a configmap from a literal value.
'''
apiVersion: v1
kind: ConfigMap
metadata:
  name: myconfigmap

data:
    key1: value1
    key2: value2.namespace_name  # to use configmap values present in a different namespace
'''

7. Namespaces: are used to group and isolate resources. each namespace has its own resources like pods, services, secrets, and configmaps.
> secret and configmap values can only be accessed by the pods in the same namespace.
> pods can communicate with each other across namespaces.
> Namespace can be used for resource isolation, access control, and resource quota.
> Namespace can be used for blue-green deployment, canary deployment, and multi-tenancy.
> volume, persistant volume and node

# NOTE: kubens and kubectx is external tool which allows for switching between namespaces and contexts respectively.

- kubectl get namespaces: displays the namespaces in the cluster.
- kubectl create namespace <namespace-name>: creates a namespace.
- kubectl apply -f <filename>: applies the configuration from a file.
- kubectl get pods -n <namespace-name>: displays the pods in a namespace.
- kubectl get services -n <namespace-name>: displays the services in a namespace.

'''
apiVersion: v1
kind: congigMap
metadata:
  name: mynamespace
  namespace: mynamespace

data:
    key1: value1
    key2: value2

'''

8. ingress: is an API object that manages external access to services in a cluster, typically HTTP. it provides load balancing, SSL termination, and name-based virtual hosting.
> The Ingress resource is a set of rules for routing external traffic to services. ingress controller is a pod running a proxy software that enforces the rules defined in the ingress resource.
> Before creating an Ingress resource, the Ingress Controller should be running in your cluster. There are several Ingress Controllers (proxy) to choose from, including Nginx, Traefik, Kong and others. In cloud aws has ALB Ingress Controller and GCP has GCE Ingress Controller.

- kubectl get ingress: displays the ingress resources in the cluster.

'''
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myingress
spec:
    tls:
    - hosts:
        - myhost.com
        secretName: mysecret
    rules:
    - host: myhost.com         # host name
        http:                   
        paths:                  # paths to route the traffic
        - path: /                # path to route the traffic
            pathType: Prefix      # type of path matching
            backend:
                service:
                    name: myservice
                    port:
                        number: 80
'''
'''
apiVersion: v1
kind: Secret
metadata:
    name: my-tls-secret
    namespace: default
type: kubernetes.io/tls
data:
    tls.crt: <base64-encoded-certificate>
    tls.key: <base64-encoded-key>
'''


9. volumes: are used to persist data in kubernetes. there are different types of volumes available in kubernetes.
1. emptyDir: is a temporary volume that is created when a pod is assigned to a node and deleted when the pod is removed from the node.
2. hostPath: mounts a file or directory from the host node's filesystem into the pod.
3. secret: mounts a secret as a volume in a pod.
4. configMap: mounts a config map as a volume in a pod.
5. persistentVolumeClaim: mounts a persistent volume claim as a volume in a pod.
6. nfs: mounts an NFS share as a volume in a pod.
7. storageClass: is used to dynamically provision persistent volumes.
8. persistentVolume: is a piece of storage in the cluster that has been provisioned by an administrator.


>> adminitrator creates persistent volume resource in the cluster. it can located locally, remotely or cloud.
>> user uses persistent volume claim to request storage from the persistent volume resource.
>> size of PV is fixed and should be initialized by admin.
>> storage class is used to dynamically provision persistent volumes based on the storage requirements.
>> a Persistent Volume Claim (PVC) can only bind to a single Persistent Volume (PV) at a time. The binding is a one-to-one mapping.
>> if same PVC is used by multiple pods, then the data will be shared between the pods.

types of access modes:
1. ReadWriteOnce: can be mounted as read-write by a single node.
2. ReadOnlyMany: can be mounted as read-only by many nodes.
3. ReadWriteMany: can be mounted as read-write by many nodes.

- kubectl get pv: displays the persistent volumes in the cluster.
- kubectl get pvc: displays the persistent volume claims in the cluster.

''' attach pvc to pod
apiVersion: v1
kind: Pod
metadata:
    name: my-pod
spec:
    containers:
    - name: my-container
        image: nginx
        volumeMounts:
        - name: my-volume
            mountPath: /path/in/container
    volumes:
    - name: my-volume
        persistentVolumeClaim:
            claimName: my-pvc-10gb
'''
''' pvc configuration
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
    name: my-pvc-10gb
spec:
    accessModes:
        - ReadWriteOnce
    resources:
        requests:
            storage: 10Gi
    storageClassName: standard  | volumeName: my-pv
'''
''' persistent volume resource congifuration
apiVersion: v1
kind: PersistentVolume
metadata:
    name: my-pv
spec:
    capacity:
        storage: 100Gi
    accessModes:
        - ReadWriteOnce
    persistentVolumeReclaimPolicy: Retain
    storageClassName: standard
    hostPath:
        path: "/mnt/data"
'''
'''dynamic pv storage class configuration
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
    name: ssd
provisioner: kubernetes.io/gce-pd
parameters:
    type: pd-ssd
'''

10. StatefulSets: is a service that can be used to deployment and scaling of a set of stateful pods (requires persistant storage to run properly). it is used to run stateful applications like databases, caches, and key-value stores.

>> StatefulSets are used to manage the deployment and scaling of a set of stateful pods. StatefulSets are used to run stateful applications like databases, caches, and key-value stores.
>> StatefulSets provide guarantees about the ordering and uniqueness of the pods. Each pod in a StatefulSet has a unique identity that is maintained across rescheduling.
>> Each pod in a StatefulSet has a unique identity that is maintained across rescheduling. 
>> The genreally pods are created in order, and each pod is created only after the previous pod is running and ready. it can over-ridden by setting the podManagementPolicy to Parallel.
>> persistent volume claim templates are used to dynamically provision persistent volumes for each pod in the StatefulSet.
>> persistent volume is retained even after the pod is deleted, and it can be reattached to a new version of same pod.
>> headless service is used to access the pods in the StatefulSet directly without load balancing.

example:
'''
apiVersion: apps/v1
kind: StatefulSet
metadata:
    name: my-statefulset
spec:
    serviceName: "my-service"
    replicas: 5
    selector:
        matchLabels:
            app: my-app
    template:
        metadata:
            labels:
                app: my-app
        spec:
            containers:
            - name: my-container
                image: nginx
                volumeMounts:
                - name: my-volume
                    mountPath: /path/in/container
    volumeClaimTemplates:
    - metadata:
            name: my-volume
        spec:
            accessModes: < "ReadWriteOnce" >
            resources:
                requests:
                    storage: 10Gi
'''

11. DaemonSets: ensures that all (or some) nodes run a copy of a pod. it is used to run a daemon on every node in the cluster.


# K8 yaml file structure:

- apiVersion:specifies the version of the kubernetes API.
- kind:specifies the type of the kubernetes resource.
- metadata:specifies the metadata of the resource like name, labels, etc.
    - name:specifies the name of the resource.
    - labels:specifies the labels of the resource. (can contain user created multiple key-value pairs)

- spec:specifies the specification depending on resource (Pod, ReplicaSet, Service,..).
    - containers: the containers running in the pod.
        - name:specifies the name of the container.
        - image:specifies the image of the container.
        - ports:specifies the ports exposed by the container.
        - volumeMounts:specifies the volumes mounted by the container.
    - volumes:specifies the volumes used by the pod.
        - name:specifies the name of the volume.
        - emptyDir:specifies an empty directory volume.
        - hostPath:specifies a host path volume.
        - secret:specifies a secret volume.
        - configMap:specifies a config map volume.
        - persistentVolumeClaim:specifies a persistent volume claim volume.
        - hostNetwork:specifies whether the pod should use the host network.
    

# NOTE: 
- apiVersion specifies which version or group of k8 api is used for communication between the services. 
- different kind of api versions:s
    1. core: v1
    kind: (types of resources in core api version)
        - Pod
        - Service
        - Namespace
        - Event
        - Endpoints
        - Node
        - Secret
        - ConfigMap
        - PersistentVolume
        - PersistentVolumeClaim

    2. apps: apps/v1
    kind: (types of resources in apps api version)
        - Deployment
        - ReplicaSet
        - StatefulSet
        - DaemonSet

    3. batch: batch/v1
    kind: (types of resources in batch api version)
        - Job
        - CronJob

    4. autoscaling: autoscaling/v1
    kind: (types of resources in autoscaling api version)
        - HorizontalPodAutoscaler

    5. networking: networking.k8s.io/v1
    kind: (types of resources in networking api version)
        - NetworkPolicy
        - Ingress

    6. storage: storage.k8s.io/v1
    kind: (types of resources in storage api version)
        - StorageClass
        - VolumeAttachment
        - StorageState



Note: Scheduling of Pods in selective nodes.
- nodeSelector: is used to schedule the pods on specific nodes based on the labels assigned to the nodes.
- affinity: is used to schedule the pods based on the affinity or anti-affinity rules.
  - nodeAffinity: is used to schedule the pods based on the affinity or anti-affinity rules with the nodes.
  - podAffinity: is used to schedule the pods based on the affinity or anti-affinity rules with other pods.
  - antiAffinity: is used to schedule the pods based on the anti-affinity rules with the nodes or other pods. 
- namespaceSelector: is used to schedule the pods on nodes with specific labels in the namespace.
- tolerations: is used to schedule the pods on nodes with taints.
