# weather-app

![Version: 0.0.1](https://img.shields.io/badge/Version-0.0.1-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.0.1](https://img.shields.io/badge/AppVersion-0.0.1-informational?style=flat-square)

This is a Helm chart for Kubernetes built to run Frontend Web weather-app-page. Helm Chart created by Arif Ginanjar (arif17ginanjar@gmail.com). Frontend Web (weather-app-page) is Created by @mili.codes (instagram)

**Homepage:** <https://gitlab.com/sayurbox-test/weather-app-chart>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Arif Ginanjar | arif17ginanjar@gmail.com | https://linkedin.com/in/gihif |

## Source Code

* <https://gitlab.com/sayurbox-test/weather-app-chart>
* <https://github.com/milicodes/weather-app-page>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| nameOverride | string | `""` | [Optional] @param `nameOverride` String to partially override weather-app.fullname template (will maintain the release name) <br /> default: `weather-app` |
| fullnameOverride | string | `""` | [Optional] @param `fullnameOverride` String to fully override weather-app.fullname template |
| imagePullSecrets | list | `[]` | [Optional] @param `imagePullSecrets` is Global Docker registry secret names as an array <br /> e.g. <br /> `imagePullSecrets:` <br /> `  - myRegistryKeySecretName` |
| commonLabels | object | `{}` | [Optional] @param `commonLabels` Add labels to all the deployed resources |
| serviceAccount.create | bool | `true` | [Optional] @param `serviceAccount.create` Specifies whether a service account should be created |
| serviceAccount.annotations | object | `{}` | [Optional] @param `serviceAccount.annotations` is Annotations to add to the service account |
| serviceAccount.name | string | `""` | [Optional] @param `serviceAccount.name` The name of the service account to use. <br /> If not set and create is true, a name is generated using the `weather-app.fullname` template |
| replicaCount | int | `1` |  |
| image.repository | string | `"nginx"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.tag | string | `""` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.type | string | `"ClusterIP"` |  |
| service.port | int | `80` |  |
| ingress.enabled | bool | `false` |  |
| ingress.className | string | `""` |  |
| ingress.annotations | object | `{}` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| ingress.tls | list | `[]` |  |
| resources | object | `{}` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.maxReplicas | int | `100` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| nodeSelector | object | `{}` |  |
| tolerations | list | `[]` |  |
| affinity | object | `{}` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.5.0](https://github.com/norwoodj/helm-docs/releases/v1.5.0)
