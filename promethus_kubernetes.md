# Prometheus Kubernetes

prometheus is a monitoring tool that scrapes metrics from different sources and stores them in a time series database.

## Architecture

1. prometheus: This is the main Prometheus server that scrapes and stores metrics. It is usually deployed as a StatefulSet or Deployment in your cluster.

2. kube-state-metrics: This is a service that listens to the Kubernetes API server and generates metrics about the state of the objects in the Kubernetes cluster. It is usually deployed as a Deployment in your cluster.

3. node-exporter: This is a daemon that collects system metrics like CPU usage, memory, disk I/O, and network statistics. It is usually deployed as a DaemonSet in your cluster so that it runs on every node.

4. metrics-server: This is an optional component that provides CPU and memory usage metrics for pods and nodes, which can be used by Kubernetes for autoscaling. It is usually deployed as a Deployment in your cluster.

5. alertmanager: This is an optional component that handles alerts sent by Prometheus server and takes care of deduplicating, grouping, and routing them to the correct receiver. It is usually deployed as a StatefulSet or Deployment in your cluster.

6. grafana: This is an optional component that provides a web interface for dashboarding and visualization of Prometheus collected metrics. It is usually deployed as a Deployment in your cluster.

7. prometheus-operator (optional): This is a Kubernetes operator that simplifies the deployment and configuration of Prometheus, Alertmanager, and related monitoring components. It introduces additional resources like ServiceMonitor and AlertmanagerConfig to describe the desired state of a Prometheus and Alertmanager setup.



- kubernetes by default doesn't support meterics collection. we need to deploy a kube-state-meterics server in the cluster to monitor Kubernetes API server Meterics (high level)like deployments, pods, nodes etc.  
- to fetch hardware metrics like CPU, memory, disk etc. we need to deploy node-exporter on each node in the cluster.
kubernetes cluster -> prometheus server -> prometheus storage -> prometheus web ui
