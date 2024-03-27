## kubernetes
kubernetes is a container orchestration tool that helps in managing containerized applications in different environments. It is an open-source platform developed by google, which automates the deployment, scaling, and management of containerized applications.

# Kubernetes Architecture
Kubernetes architecture consists of a master node and a worker node. 
- The master node is responsible for managing the worker nodes and scheduling pods running on them. 
- The worker nodes are responsible for running the containers or pods.

# Master Node
The master node consists of the following components:
- API Server: It is the front-end of the control plane. It exposes the kubernetes API, which is used by the clients to interact with the cluster.
- Controller Manager: It is responsible for running the controller processes, which are responsible for maintaining the desired state of the cluster.
- Scheduler: It is responsible for scheduling the pods on the worker nodes based on the resource requirements and constraints.
- etcd: It is a distributed key-value store that stores the cluster state. 

# Worker Node
The worker node consists of the following components:
- Kubelet: It is responsible for managing containers running on the node and communication between worker node and master node.
- Kube Proxy: It is responsible for routing traffic to the pods from outside the cluster (basically internet).
- Container Runtime: Runtime used to run the containers.(DOCKER or containerd)
- Pod: It is the smallest unit of deployment in kubernetes. It consists of one or more containers that share the same network and storage. (running containers)


# K8 Commands
kubectl: It is a command-line tool used to interact with the kubernetes cluster. 

types of resources in k8s:
1. Pods : smallest unit of deployment in k8s
2. ReplicaSets : ensures specific number of pods are running in cluster
3. Deployments : manages ReplicaSets and Pods
4. Services : provides networking to the pods


commands:

- kubectl version: It displays the client and server version of kubectl.
- kubectl help: It displays the help information for kubectl.
- kubectl get <resource_type> <resource_name>: It displays the resources in the cluster.
- kubectl create: It creates a resource in the cluster.
- kubectl apply: It applies the configuration to the cluster.
- kubectl delete <resource_type> <resource_name>: It deletes a resource from the cluster.
- kubectl describe <resource_type> <resource_name>: It displays detailed information about a resource.
- kubectl logs: It displays the logs of a container in a pod.
- kubectl exec: It executes a command in a container in a pod.
- kubectl run: It creates a new pod or deployment.
- kubectl expose: It exposes a deployment as a service.
- kubectl scale: It scales a deployment.


- kubectl get nodes: It displays the nodes in the cluster. (less information)
- kubectl get nodes -o wide: It displays the nodes in the cluster with additional information.
- kubectl get pods: It displays the pods in the cluster.
- kubectl get services: It displays the services in the cluster.

- kubectl get deployments: It displays the deployments in the cluster.
- kubectl get replicasets: It displays the replica sets in the cluster.
- kubectl create deployment <deployment-name> --image=<image-name>: It creates a deployment with the specified image.
- kubectl expose deployment <deployment-name> --port=<port>: It exposes a deployment as a service on the specified port.




- kubectl create -f <filename>: It creates a resource from a file.
- kubectl apply -f <filename>: It applies the configuration from a file.
- kubectl delete -f <filename>: It deletes a resource from a file.
- kubectl describe <resource-name>: It displays detailed information about a resource.
- kubectl scale --replicas=<number> <fileename>: It scales a deployment to the specified number of replicas.

- kubectl logs <pod-name>: It displays the logs of a pod.






# K8 yaml file structure:

- apiVersion: It specifies the version of the kubernetes API.
- kind: It specifies the type of the kubernetes resource.
- metadata: It specifies the metadata of the resource like name, labels, etc.
    - name: It specifies the name of the resource.
    - labels: It specifies the labels of the resource. (can contain user created multiple key-value pairs)

- spec: It specifies the specification depending on resource (Pod, ReplicaSet, Service,..).
    - containers: the containers running in the pod.
        - name: It specifies the name of the container.
        - image: It specifies the image of the container.
        - ports: It specifies the ports exposed by the container.
        - volumeMounts: It specifies the volumes mounted by the container.
    - volumes: It specifies the volumes used by the pod.
        - name: It specifies the name of the volume.
        - emptyDir: It specifies an empty directory volume.
        - hostPath: It specifies a host path volume.
        - secret: It specifies a secret volume.
        - configMap: It specifies a config map volume.
        - persistentVolumeClaim: It specifies a persistent volume claim volume.
        - hostNetwork: It specifies whether the pod should use the host network.
    

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
    '''

