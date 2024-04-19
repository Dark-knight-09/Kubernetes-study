## kubernetes
kubernetes is a container orchestration tool that helps in managing containerized applications in different environments.is an open-source platform developed by google, which automates the deployment, scaling, and management of containerized applications.

# Kubernetes Architecture
Kubernetes architecture consists of a master node and a worker node. 
- The master node is responsible for managing the worker nodes and scheduling pods running on them. 
- The worker nodes are responsible for running the containers or pods.

# Master Node
The master node consists of the following components:
- API Server:is the front-end of the control plane.exposes the kubernetes API, which is used by the clients to interact with the cluster.
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


commands:

- kubectl version:displays the client and server version of kubectl.
- kubectl help:displays the help information for kubectl.
- kubectl get <resource_type> <resource_name>:displays the resources in the cluster.
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



basic example for pod yaml file:
'''
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
    containers:
    - name: mycontainer
        image: nginx
        ports:
        - containerPort: 80

    '''

basic example for service yaml file:
'''
apiVersion: v1
kind: Service
metadata:
  name: myservice   
spec:
    selector:
        app: myapp
    ports:
        - protocol: TCP
        port: 80
        targetPort: 80
    type: LoadBalancer
    '''

basic example for replica set yaml file:
'''
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myreplicaset

spec:
    replicas: 3
    selector:
        matchLabels:
            app: myapp
    template:
        metadata:
            labels:
                app: myapp
        spec:
            containers:
            - name: mycontainer
              image: nginx
            - env:
                - name: MY_ENV
                  value: myvalue    | valueFrom: 
                                    |   secretKeyRef:
                                    |           name: mysecret
                                    |           key: mykey
                                          
    '''

