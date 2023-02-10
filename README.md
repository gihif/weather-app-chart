# weather-app

![Version: 0.0.3](https://img.shields.io/badge/Version-0.0.3-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.0.3](https://img.shields.io/badge/AppVersion-0.0.3-informational?style=flat-square)

This is a Helm chart for Kubernetes built to run Frontend Web weather-app-page. Helm Chart created by Arif Ginanjar (arif17ginanjar@gmail.com). Frontend Web (weather-app-page) is Created by @mili.codes (instagram)

**Homepage:** <https://gitlab.com/sayurbox-test/weather-app-chart>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Arif Ginanjar | arif17ginanjar@gmail.com | https://linkedin.com/in/gihif |

## Source Code

* <https://gitlab.com/sayurbox-test/weather-app-chart>
* <https://github.com/milicodes/weather-app-page>

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| https://charts.bitnami.com/bitnami | common | 1.10.x |

## How to use Chart

### Prerequisite

* Have a cluster with nodes that have the following labels
  ``` bash
  app-deployment = true
  db-deployment = false
  monitoring-deployment = false
  ```
  > if you don't have nodes with those labels, you can override the default values.yaml in yours

* Already installed `kubectl`

* Already installed `helm`

### Guide

Follow these steps to be able to install this chart:

* First create namespace with the following command
```bash
kubectl create namespace weather-app
```

* Now, lets install the charts with this following command
```bash
helm upgrade --install --namespace weather-app --version 0.0.3 \
  weather-app https://gitlab.com/sayurbox-test/weather-app-chart/-/archive/0.0.3/weather-app-chart-0.0.3.tar.gz
```

* Oke, now run this following commands
```bash
export POD_NAME=$(kubectl get pods --namespace weather-app -l "app.kubernetes.io/name=weather-app,app.kubernetes.io/instance=weather-app" -o jsonpath="{.items[0].metadata.name}")
export CONTAINER_PORT=$(kubectl get pod --namespace weather-app $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
echo "Visit http://127.0.0.1:8080 to use your application"
kubectl --namespace weather-app port-forward $POD_NAME 8080:$CONTAINER_PORT
```

* Then, Visit this URL http://127.0.0.1:8080

* Wheather app now can be accessed

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| nameOverride | string | `""` | @param `nameOverride` String to partially override weather-app.fullname template (will maintain the release name) <br /> default: `weather-app` |
| fullnameOverride | string | `""` | @param `fullnameOverride` String to fully override weather-app.fullname template |
| imagePullSecrets | list | `[]` | @param `imagePullSecrets` is Global Docker registry secret names as an array <br /> e.g. <br /> `imagePullSecrets:` <br /> `  - myRegistryKeySecretName` |
| commonLabels | object | `{}` | @param `commonLabels` Add labels to all the deployed resources |
| commonAnnotations | object | `{}` | @param `commonAnnotations` Add annotations to all the deployed resources |
| serviceAccount.create | bool | `true` | @param `serviceAccount.create` Specifies whether a service account should be created |
| serviceAccount.annotations | object | `{}` | @param `serviceAccount.annotations` is Annotations to add to the service account |
| serviceAccount.name | string | `""` | @param `serviceAccount.name` The name of the service account to use. <br /> If not set and create is true, a name is generated using the `weather-app.fullname` template |
| image.registry | string | `"registry.gitlab.com/sayurbox-test"` | @param `image.registry` is Container Registry where Weather App image stored |
| image.repository | string | `"weather-app-chart/web"` | @param `image.repository` is Repository image name of Weather App image stored |
| image.tag | string | `""` | @param `image.tag` to Overrides the image tag whose default is the chart appVersion. |
| image.command | string | `""` | @param `image.command` to Overrides the default image command. |
| image.pullPolicy | string | `"IfNotPresent"` | @param `image.pullPolicy` for Specifies pull policy method <br /> Defaults to 'Always' if image tag is 'latest', else set to 'IfNotPresent' <br /> ref: https://kubernetes.io/docs/user-guide/images/#pre-pulling-images |
| replicaCount | int | `1` | @param `replicaCount` Number of Weather App replicas to deploy |
| updateStrategy | object | `{"rollingUpdate":{"maxSurge":"25%","maxUnavailable":"25%"},"type":"RollingUpdate"}` | @param `updateStrategy` is a Strategy how deployment will Rollout the Updates |
| podAnnotations | object | `{}` | @param `podAnnotations` Annotations for Weather App pods <br /> ref: https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/ |
| podAffinityPreset | string | `""` | @param `podAffinityPreset` Pod affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard` <br /> ref: https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity |
| podAntiAffinityPreset | string | `""` | @param `podAntiAffinityPreset` Pod anti-affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard` <br /> Ref: https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity |
| nodeAffinityPreset.type | string | `""` | @param `nodeAffinityPreset.type` Node affinity preset type. Ignored if `affinity` is set. Allowed values: `soft` or `hard` |
| nodeAffinityPreset.key | string | `""` | @param `nodeAffinityPreset.key` Node label key to match Ignored if `affinity` is set. <br /> E.g. <br /> key: "kubernetes.io/e2e-az-name" |
| nodeAffinityPreset.values | list | `[]` | @param `nodeAffinityPreset.values` Node label values to match. Ignored if `affinity` is set. <br /> E.g. <br /> `values:` <br /> `  - e2e-az1` <br /> `  - e2e-az2` |
| affinity | object | `{}` | @param `affinity` Affinity for pod assignment <br /> ref: https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity <br /> Note: podAffinityPreset, podAntiAffinityPreset, and  nodeAffinityPreset will be ignored when it's set <br /> `affinity:` <br /> `  nodeAffinity:` <br /> `    requiredDuringSchedulingIgnoredDuringExecution:` <br /> `      nodeSelectorTerms:` <br /> `        - matchExpressions:` <br /> `            - key: app-deployment` <br /> `              operator: In` <br /> `              values:` <br /> `                - "true"` <br /> |
| nodeSelector | object | `{}` | @param `nodeSelector` Node labels for pod assignment. Evaluated as a template. <br /> Ref: https://kubernetes.io/docs/user-guide/node-selection/ |
| tolerations | list | `[]` | @param `tolerations` Tolerations for pod assignment. Evaluated as a template. <br /> Ref: https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/ |
| podSecurityContext.enabled | bool | `false` | @param `podSecurityContext.enabled` Enabled Weather app pods' Security Context |
| podSecurityContext.fsGroup | int | `1001` | @param `podSecurityContext.fsGroup` Set Weather app pod's Security Context fsGroup |
| podSecurityContext.sysctls | list | `[]` | @param `podSecurityContext.sysctls` sysctl settings of the Weather App pods <br /> sysctl settings <br /> Example: <br /> `sysctls:` <br /> `- name: net.core.somaxconn` <br /> `  value: "10000"` <br /> |
| securityContext | object | `{}` | @param securityContext Set Weather app container's Security Context Example: <br /> `securityContext:` <br /> `  capabilities:` <br /> `    drop:` <br /> `    - ALL` <br /> `  readOnlyRootFilesystem: true` <br /> `  runAsNonRoot: true` <br /> `  runAsUser: 1000` |
| containerPorts.name | string | `"http"` | @param `containerPorts.name` is a port name of Weather app container |
| containerPorts.number | int | `80` | @param `containerPorts.number` is a port number of Weather app container |
| containerPorts.protocol | string | `"TCP"` | @param `containerPorts.protocol` is a port number of Weather app container |
| livenessProbe.path | string | `"/"` | @param `livenessProbe.path` is path of livenessProbe |
| livenessProbe.initialDelaySeconds | int | `30` | @param `livenessProbe.initialDelaySeconds` Initial delay seconds for livenessProbe |
| livenessProbe.timeoutSeconds | int | `5` | @param `livenessProbe.periodSeconds` Period seconds for livenessProbe |
| livenessProbe.periodSeconds | int | `10` | @param `livenessProbe.timeoutSeconds` Timeout seconds for livenessProbe |
| livenessProbe.failureThreshold | int | `6` | @param `livenessProbe.failureThreshold` Failure threshold for livenessProbe |
| livenessProbe.successThreshold | int | `1` | @param `livenessProbe.successThreshold` Success threshold for livenessProbe |
| readinessProbe.path | string | `"/"` | @param `readinessProbe.path` is path of readinessProbe |
| readinessProbe.initialDelaySeconds | int | `5` | @param `readinessProbe.initialDelaySeconds` Initial delay seconds for readinessProbe |
| readinessProbe.timeoutSeconds | int | `3` | @param `readinessProbe.periodSeconds` Period seconds for readinessProbe |
| readinessProbe.periodSeconds | int | `5` | @param `readinessProbe.timeoutSeconds` Timeout seconds for readinessProbe |
| readinessProbe.failureThreshold | int | `3` | @param `readinessProbe.failureThreshold` Failure threshold for readinessProbe |
| readinessProbe.successThreshold | int | `1` | @param `readinessProbe.successThreshold` Success threshold for readinessProbe |
| terminationGracePeriodSeconds | int | `90` | @param `terminationGracePeriodSeconds` is a specific time in seconds the pods will terminate |
| resources.limits | object | `{"cpu":"150m","memory":"128Mi"}` | @param `resources.limits` The resources limits for the Weather app container <br /> Example: <br /> `limits:` <br /> `  cpu: 100m` <br /> `  memory: 128Mi` |
| resources.requests | object | `{"cpu":"50m","memory":"80Mi"}` | @param `resources.requests` The requested resources for the Weather app container <br /> Examples: <br /> `requests:` <br /> `  cpu: 100m` <br /> `  memory: 128Mi` |
| configMap.serverBlock | string | `"server {\n  listen 80;\n  location / {\n    root   /usr/share/nginx/html;\n    index  index.html index.htm;\n    try_files $uri $uri/ /index.html;\n  }\n  error_page   502 503 504 500  /50x.html;\n  location = /50x.html {\n    root   /usr/share/nginx/html;\n  }\n}\n"` | @param `configMap.serverBlock` Custom server block to be added to NGINX configuration |
| configMap.envVariables | object | `{"ENVIRONMENT":"production","PROJECT_NAME":"weather-app"}` | @param `configMap.envVariables` is All required variables will set as Environment Variables to Weather App container |
| service.type | string | `"ClusterIP"` | @param `service.type` Service type |
| service.portName | string | `"http"` | @param `service.portName` is a name of port will exposed  |
| service.portNumber | int | `80` | @param `service.portNumber` is a number of port will exposed |
| service.portProtocol | string | `"TCP"` | @param `service.portProtocol` is a protocol of port will exposed |
| service.sessionAffinity | string | `"None"` | @param `service.sessionAffinity` is session affinity of service |
| autoscaling.enabled | bool | `true` | @param `autoscaling.enabled` Enable autoscaling for Weather app deployment |
| autoscaling.minReplicas | int | `5` | @param `autoscaling.minReplicas` Minimum number of replicas to scale back |
| autoscaling.maxReplicas | int | `10` | @param `autoscaling.maxReplicas` Maximum number of replicas to scale out |
| autoscaling.targetCPU | int | `60` | @param `autoscaling.targetCPU` Target CPU utilization percentage |
| autoscaling.targetMemory | int | `60` | @param `autoscaling.targetMemory` Target Memory utilization percentage |
| autoscaling.customMetrics | list | `[]` | @param `autoscaling.customMetrics` to add another autoscaling matrics besides CPU and Memory <br /> Examples: <br /> `metrics:` <br /> `- type: Pods` <br /> `  pods:` <br /> `    metric:` <br /> `      name: packets-per-second` <br /> `    target:` <br /> `      type: AverageValue` <br /> `      averageValue: 1k` |
| pdb.create | bool | `true` | @param `pdb.create` Created a PodDisruptionBudget |
| pdb.minAvailable | int | `2` | @param `pdb.minAvailable` Min number of pods that must still be available after the eviction |
| pdb.maxUnavailable | int | `0` | @param `pdb.maxUnavailable` Max number of pods that can be unavailable after the eviction |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.5.0](https://github.com/norwoodj/helm-docs/releases/v1.5.0)
