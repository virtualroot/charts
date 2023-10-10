# structurizr

![Version: 0.2.1](https://img.shields.io/badge/Version-0.2.1-informational?style=flat-square) ![AppVersion: 3194](https://img.shields.io/badge/AppVersion-3194-informational?style=flat-square)

The Structurizr Helm chart deploys Structurizr On premise flavor. Structurizr is a web-based rendering tool designed to help software development teams create software architecture diagrams and documentation.

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Affinity settings for pod assignment. |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `100` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"structurizr/onpremises"` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.className | string | `""` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"structurizr.local"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| ingress.tls | list | `[]` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| replicaCount | int | `1` | Specify the number of replicas |
| resources | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.port | int | `8080` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| tolerations | list | `[]` | Tolerations for pod assignment. Useful for nodes with taints. |
| volumes | list | `[]` | List of additional volumes to be added to the pods. |
| volumeMounts | list | `[]` | Specifies where to mount the volumes in the pod. |
| properties | string | (multi-line string) | Custom properties configuration for Structurizr. |
| users | string | (multi-line string) | Specifies user credentials for Structurizr. |
| roles | string | (multi-line string) | Specifies user roles for Structurizr. |
| saml | string | (multi-line string) | SAML identity provider metadata configuration for Structurizr authentication. |
| log4j2 | string | (multi-line string) | Configuration settings for the logging system using Log4j2. |
| env | list | `[]` | List of environment variables to be set for the Structurizr pod. |

## Additional Configuration Details:

### `volumes` and `volumeMounts`:
You can define additional volumes to attach to the pod and specify where they are mounted. For example:

```yaml
volumes:
  - name: my-storage
    persistentVolumeClaim:
      claimName: my-pvc
volumeMounts:
  - name: my-storage
    mountPath: /path/in/container
```

### `properties`, `users`, `roles`, and `saml-idp-metadata`:
These fields allow you to define multi-line strings for configurations. For instance, `properties` can be used to set Structurizr-specific configurations:

```yaml
properties: |
  structurizr.redis.password=${REDIS_PASSWORD}
  structurizr.authentication=saml
```
Similar patterns can be used for `users`, `roles`, and `saml-idp-metadata` fields.

### `env`:
You can specify additional environment variables for the Structurizr application. For instance:

```yaml
env:
  - name: STRUCTURIZR_DATA_DIRECTORY
    value: "/usr/local/structurizr"
```
This can be useful to configure aspects of Structurizr using environment variables.

## TODO

- [ ] Encryption
- [ ] Authentication
  - [ ] File
  - [ ] LDAP
  - [x] SAML
- [ ] Redis sessions
- [ ] Bucket data
