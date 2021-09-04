# kube-pires

![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)  ![Version: 1.1.0](https://img.shields.io/badge/Version-1.1.0-informational?style=flat-square)

Helm chart of example

# Prerequisites

## Kubectl

Install ``kubectl`` command.

```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl

chmod +x ./kubectl

sudo mv ./kubectl /usr/local/bin/kubectl

kubectl version --client
```

## Helm

Install ``helm`` command.

```bash
VERSION=v3.2.4
HELM_TAR_FILE=helm-$VERSION-linux-amd64.tar.gz

wget https://get.helm.sh/${HELM_TAR_FILE}

tar -xvzf ${HELM_TAR_FILE}

chmod +x linux-amd64/helm

sudo cp linux-amd64/helm /usr/bin/helm

rm -rf ${HELM_TAR_FILE} linux-amd64

helm version
```

# Installing the Chart

* First, access a Kubernetes cluster.

* Change the values according to the need of the environment in ``kube-pires/values.yaml`` file.

* Create namespace ``kube-pires`` in Kubernetes cluster.

```bash
kubectl create namespace kube-pires
```

* Test the installation with command:

```bash
helm upgrade --install kube-pires -f kube-pires/values.yaml kube-pires -n kube-pires --dry-run
```

* To install/upgrade the chart with the release name `kube-pires`:

```bash
helm upgrade --install kube-pires -f kube-pires/values.yaml kube-pires -n kube-pires
```

These commands install kube-pires on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

* List all releases using follow command:

```bash
helm list --all --all-namespaces

#or

helm list -f 'kube-pires' -n kube-pires
```

* See the history of versions of ``kube-pires`` application with command.

```bash
helm history kube-pires -n kube-pires
```

## Uninstalling the Chart

To uninstall/delete the `kube-pires` deployment:

```bash
helm uninstall kube-pires -n kube-pires
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

> If the application is removed without the ``--keep-history`` option, the history will be lost and it will not be possible to roll back.

## Parameters

The following tables lists the configurable parameters of the chart and their default values.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `20` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"nginx"` |  |
| image.tag | string | `"1.19.2"` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths | list | `[]` |  |
| ingress.tls | list | `[]` |  |
| livenessProbe.failureThreshold | int | `3` |  |
| livenessProbe.initialDelaySeconds | int | `20` |  |
| livenessProbe.path | string | `"/fail"` |  |
| livenessProbe.periodSeconds | int | `10` |  |
| livenessProbe.successThreshold | int | `1` |  |
| livenessProbe.timeoutSeconds | int | `5` |  |
| mySecret.enabled | bool | `true` |  |
| mySecret.my_secret_distributed_tracing_enabled | string | `"true"` |  |
| mySecret.my_secret_high_security | string | `"false"` |  |
| mySecret.my_secret_license_key | string | `"mysecurepassword2"` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| readinessProbe.failureThreshold | int | `3` |  |
| readinessProbe.initialDelaySeconds | int | `20` |  |
| readinessProbe.path | string | `"/fail"` |  |
| readinessProbe.periodSeconds | int | `10` |  |
| readinessProbe.successThreshold | int | `1` |  |
| readinessProbe.timeoutSeconds | int | `5` |  |
| replicaCount | int | `20` |  |
| resources.limits.cpu | string | `"300m"` |  |
| resources.limits.memory | string | `"512Mi"` |  |
| resources.requests.cpu | string | `"100m"` |  |
| resources.requests.memory | string | `"128Mi"` |  |
| securityContext | object | `{}` |  |
| service.port | int | `80` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| tolerations | list | `[]` |  |
| updateStrategy.rollingUpdate.maxSurge | int | `6` |  |
| updateStrategy.rollingUpdate.maxUnavailable | int | `0` |  |
| updateStrategy.type | string | `"RollingUpdate"` |  |

Change the values according to the need of the environment in ``kube-pires/values.yaml`` file.

# Documentation of Helm Chart

* Install helm-docs following the instructions on this page https://github.com/norwoodj/helm-docs

* Generate docs with helm-docs for this chart.

```bash
cd kube-pires

helm-docs
```

The markdown generation is entirely gotemplate driven. The tool parses metadata from charts and generates a number of sub-templates that can be referenced in a template file (by default ``README.md.gotmpl``). If no template file is provided, the tool has a default internal template that will generate a reasonably formatted README.