Helm Charts – Kubernetes Package Manager
 What is Helm?

Helm is the package manager for Kubernetes.
Just like apt is used for Ubuntu and yum for CentOS, Helm is used to install, upgrade, manage, and delete Kubernetes applications.

OS Package Managers Example
apt install git     # Ubuntu
yum install git     # CentOS

Kubernetes Package Manager
helm install <chart>

 Why do we need Helm?

In Kubernetes:

An application may require multiple YAML files

Deployment

Service

Ingress

ConfigMap

Secret

PVC

If:

1 application = 6 YAML files

1 project = 6 environments (dev, test, stage, prod, etc.)

 Total files = 36+ YAML files

Managing this manually is hard, error-prone, and repetitive.

 Helm solves this problem by:

Packaging all Kubernetes YAMLs into one chart

Reusing templates

Changing values per environment using values.yaml

 Helm Chart Structure

A Helm chart follows a fixed directory structure:

my-chart/
├── templates/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   ├── configmap.yaml
│   ├── secret.yaml
│   ├── pvc.yaml
├── Chart.yaml
├── values.yaml
├── values-dev.yaml
├── values-test.yaml
├── values-prod.yaml

 Description of Files

Chart.yaml

Metadata about the chart (name, version, description)

templates/

Contains Kubernetes YAML templates

values.yaml

Default values used in templates

values-dev/test/prod.yaml

Environment-specific values

 How Helm Works (Simple Flow)

Templates contain variables (e.g., replicas, image, ports)

Values are provided via values.yaml

Helm renders templates → generates final Kubernetes YAML

YAML is applied to the cluster

 Helm Commands
 List Helm Releases
helm list

 Install a Chart (First Time)
helm install <release-name> <chart-path>


Example:

helm install nagasai-app-release ./my-chart

 Upgrade a Chart (Next Deployments)
helm upgrade <release-name> <chart-path>


Example:

helm upgrade nagasai-app-release ./my-chart

 Override Values Using --set
helm upgrade nagasai-app-release ./my-chart --set replicas=4

 Use Environment-Specific Values Files
helm upgrade nagasai-app-release ./my-chart --values values.yaml
helm upgrade nagasai-app-release ./my-chart --values values-dev.yaml
helm upgrade nagasai-app-release ./my-chart --values values-test.yaml
helm upgrade nagasai-app-release ./my-chart --values values-prod.yaml

 Delete a Helm Release
helm delete nagasai-app-release

 Best Practices

Use separate values files for each environment

Keep templates generic and reusable

Use helm lint before installing

Use helm upgrade --install for CI/CD pipelines