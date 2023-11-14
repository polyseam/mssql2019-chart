# MSSQL Helm Chart

This Helm chart deploys Microsoft SQL Server 2019 on a Kubernetes cluster using the Helm package manager. The chart is available in the Polyseam repository.

## Chart Repository

The chart is hosted in the Polyseam chart repository. To add this repository to your Helm setup, run the following command:

```bash
helm repo add polyseam https://polyseam.github.io/mssql2019-chart/
helm repo update
```

## Prerequisites

Kubernetes 1.12+
Helm 3.0+
PV provisioner support in the underlying infrastructure (if persistence is needed)
cert-manager v1.6.0+ (if TLS is needed)

## Installing the Chart

To install the chart with the release name my-mssql:

```bash
helm install my-mssql polyseam/mssql2019-chart
```
The command deploys MSSQL on the Kubernetes cluster in the default configuration. The Parameters section lists the parameters that can be configured during installation.

## Uninstalling the Chart

To uninstall/delete the my-mssql deployment:

```bash
helm delete my-mssql
This command removes all the Kubernetes components associated with the chart and deletes the release.
```
## Parameters

The following table lists the configurable parameters of the MSSQL chart and their default values.

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `name` | Name of the MSSQL deployment | `mssql` |
| `namespace` | Kubernetes namespace for MSSQL deployment | `mssql` |
| `appLabel` | Application label for MSSQL | `mssql` |
| `serviceName` | Name of the MSSQL service | `mssql` |
| `replicas` | Number of MSSQL replicas | `1` |
| `securityContext.fsGroup` | File system group ID for the MSSQL pod | `10001` |
| `container.name` | Container name for MSSQL | `mssql` |
| `container.image` | MSSQL container image | `"mcr.microsoft.com/mssql/server:2019-latest"` |
| `service.name` | Name of the MSSQL service | `mssql-0` |
| `service.namespace` | Namespace of the MSSQL service | `mssql` |
| `service.selector.podName` | Selector pod name for the service | `mssql-0` |
| `service.ports.port` | Port number for the service | `1433` |
| `service.ports.targetPort` | Target port number for the service | `1433` |
| `certificate.name` | Name of the certificate | `mssql-certs` |
| `certificate.namespace` | Namespace of the certificate | `mssql` |
| `certificate.secretName` | Secret name for the certificate | `mssql-certs-secret` |
| `certificate.commonName` | Common name for the certificate | `"my-mssql-hostname.com"` |
| `certificate.dnsNames` | DNS names associated with the certificate | `[ "my-mssql-hostname.com", "mssql-0.mssql.svc.cluster.local" ]` |
| `configMap.name` | Name of the ConfigMap | `mssql` |
| `configMap.namespace` | Namespace of the ConfigMap | `mssql` |
| `configMap.data.mssqlConfLines` | Configuration lines for MSSQL | `[ "[EULA]", "accepteula = Y", "accepteulaml = Y", ..., "forceencryption = 0" ]` |

*Note: See `values.yaml` for a full list of configurable parameters.*




## Configuration and Installation Details
### Persistence
The chart mounts a PersistentVolume to store the data. The volume is created using dynamic volume provisioning. You can specify the size of the persistent volume in the values.yaml file.

### Customizing the Chart Before Installing
To edit the default configuration, use:

```bash
helm show values polyseam/mssql2019-chart > values.yaml
```
Edit the values.yaml file as needed and then install the chart with the updated configuration:

```bash
helm install my-mssql polyseam/mssql2019-chart -f values.yaml
```
### TLS/SSL Configuration
If you require TLS/SSL, ensure that cert-manager is installed in your cluster and configure the certificates in the values.yaml file.

## Additional Information
For more information on working with MSSQL in Kubernetes, visit MSSQL Kubernetes documentation.
For more details on using Helm, see Helm documentation.
