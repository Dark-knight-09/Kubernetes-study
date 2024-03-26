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

commands:

- kubectl version: It displays the client and server version of kubectl.
- kubectl help: It displays the help information for kubectl.

- kubectl get nodes: It displays the nodes in the cluster. (less information)
- kubectl get nodes -o wide: It displays the nodes in the cluster with additional information.
- kubectl get pods: It displays the pods in the cluster.
- kubectl get services: It displays the services in the cluster.











# K8 yaml file structure:

- apiVersion: It specifies the version of the kubernetes API.
- kind: It specifies the type of the kubernetes resource.
- metadata: It specifies the metadata of the resource like name, labels, etc.
    - name: It specifies the name of the resource.
    - labels: It specifies the labels of the resource. (can contain user created multiple key-value pairs)

- spec: It specifies the specification of the resource.
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
    

basic example:
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