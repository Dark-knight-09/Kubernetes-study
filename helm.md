## HELM

Helm is a package manager for Kubernetes that helps you manage and deploy applications on a Kubernetes cluster. It also provides features like dependency management, templating, and rollback, making it a powerful tool for managing your Kubernetes applications.

Helm uses a client-server architecture, where the Helm client interacts with the Tiller server (helm server running on the Kubernetes cluster interactive kubernetes api). The Helm client is responsible for managing charts and releases, while Tiller is responsible for deploying and managing the releases on the cluster.

Here are some key concepts in Helm:
1. Chart: A Helm package that contains all the Kubernetes resources necessary to run an application, such as deployments, services, and configmaps.
2. Release: An instance of a chart deployed on a Kubernetes cluster.
3. Repository: A collection of charts that can be shared and installed by the Helm client.
4. Values: A set of configuration values that can be passed to a chart during installation to customize its behavior.
5. Template: A Go template that defines the Kubernetes resources in a chart. Helm uses these templates to generate the actual Kubernetes manifests.

file structure of a helm chart:
``` 
mychart/
  Chart.yaml
  values.yaml
  charts/
  templates/
    deployment.yaml
    service.yaml
    configmap.yaml
    NOTES.txt
    Ingress.yaml
    _helpers.tpl

```
- Chart.yaml: Contains metadata about the chart, such as its name, version, and description.
- values.yaml: Contains the default configuration values for the chart.
- charts/: Contains any subcharts that the main chart depends on.
- templates/: Contains the Go templates that define the Kubernetes resources in the chart.


basic commands:
- helm repo add <repo-name> <repo-url> # add a helm repository
- helm repo update # update the list of available charts from the repositories
- helm search repo <chart-name> # search for a chart in the repositories
- helm install <chart-name> <release-name> # install a chart as a release
- helm list # list all releases
- helm status <release-name> # get the status of a release
- helm upgrade <release-name> <chart-name> # upgrade a release to a new version of the chart
- helm rollback <release-name> <revision-number> # rollback a release to a previous version
- helm uninstall <release-name> # uninstall a release
- helm show values <chart-name> # show the default values for a chart
- helm show chart <chart-name> # show information about a chart
- helm show readme <chart-name> # show the README for a chart
- helm lint <chart-directory> # lint a chart 
- helm package <chart-directory> # package a chart into a tarball
- helm template <chart-name> # render the templates in a chart
- helm history <release-name> # show the history of a release
- helm get values <release-name> # get the values of a release
- helm get all <release-name> # get all information about a release

