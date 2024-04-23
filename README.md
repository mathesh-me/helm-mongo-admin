# Mongo Express Admin Interface Helm Chart

This Helm chart will deploys Mongo Express Admin Interface on a Kubernetes cluster.

## Prerequisites

- Kuberbetes Cluster Installed
- Helm installed

## Installation

To install the Chart, use the following command:

```bash
helm install release-name ./mongo-express-interface
```
Don't forget to replace `release-name` with the desired release name.

## Uninstallation

To uninstall the Chart, use the following command:

```bash
helm uninstall release-name
```
Don't forget to replace `release-name` with the release name used during installation.

## Parameters Configuration

The following table lists the configurable parameters of the mongo-express-interface chart and their default values:

| Parameter                           | Description                                    | Default                      |
|-------------------------------------|------------------------------------------------|------------------------------|
| `deployments.database.replicaCount` | Number of database replicas                   | `1`                          |
| `deployments.database.pod.name`     | Name of the database pod                       | `db-pod`                     |
| `deployments.database.pod.container.name` | Name of the database container           | `db-container`               |
| `deployments.database.pod.container.image.repository` | Database container image repository | `mongo` |
| `deployments.database.pod.container.image.tag` | Database container image tag             | `5.0`                        |
| `deployments.database.pod.container.ports.containerPort` | Port on which the database container listens | `27017`             |
| `deployments.database.pod.container.volumeMounts.mountPath` | Path where the database data is mounted | `/data/db`           |
| `deployments.database.pod.container.env.username` | Environment variable for MongoDB admin username | `ME_CONFIG_MONGODB_ADMINUSERNAME` |
| `deployments.database.pod.container.env.password` | Environment variable for MongoDB admin password | `ME_CONFIG_MONGODB_ADMINPASSWORD` |
| `deployments.web.replicaCount`     | Number of web replicas                         | `1`                          |
| `deployments.web.pod.name`         | Name of the web pod                             | `web-pod`                    |
| `deployments.web.pod.container.name` | Name of the web container                     | `web-container`              |
| `deployments.web.pod.container.image.repository` | Web container image repository           | `mongo-express`              |
| `deployments.web.pod.container.image.tag` | Web container image tag                   | `latest`                     |
| `deployments.web.pod.container.ports.containerPort` | Port on which the web container listens | `8081`                     |
| `deployments.web.pod.container.env.server` | Environment variable for MongoDB server | `ME_CONFIG_MONGODB_SERVER`   |
| `service.db.type`                   | Type of service for the database               | `ClusterIP`                  |
| `service.db.ports.protocol`         | Protocol for the database service              | `TCP`                        |
| `service.db.ports.port`             | Port for the database service                  | `27017`                      |
| `service.db.ports.targetPort`       | Target port for the database service           | `27017`                      |
| `service.web.type`                  | Type of service for the web                     | `NodePort`                   |
| `service.web.ports.protocol`        | Protocol for the web service                    | `TCP`                        |
| `service.web.ports.port`            | Port for the web service                        | `8081`                       |
| `service.web.ports.targetPort`      | Target port for the web service                 | `8081`                       |
| `service.web.ports.nodePort`        | Node port for the web service                   | `30111`                      |
| `secret.type`                       | Type of secret                                  | `Opaque`                     |
| `secret.username`                   | Username for the secret                         | `user101`                    |
| `secret.password`                   | Password for the secret                         | `pass101`                    |
| `persistentVolume.accessModes`      | Access modes for the persistent volume          | `ReadWriteMany`              |
| `persistentVolume.storage`          | Storage size for the persistent volume          | `0.5Gi`                      |
| `persistentVolume.localPath`        | Local path for the persistent volume            | `/storage/mongo`             |
| `persistentVolume.host.name`        | Host name for the persistent volume             | `minikube`                   |
| `persistentVolumeClaim.accessModes` | Access modes for the persistent volume claim    | `ReadWriteMany`              |
| `persistentVolumeClaim.resourceRequest` | Resource request for the persistent volume claim | `0.5Gi`                   |
| `persistentVolumeClaim.storageClassName` | Storage class name for the persistent volume claim | `""`                      |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:

```bash
helm install my-mongo-express ./mongo-express-interface \
  --set deployments.database.replicaCount=3 \
  --set service.web.type=LoadBalancer
```

## Usage

To access the Mongo Express Admin Interface, you can use the following command:

```bash
http://<node-ip>:30111
```
Don't forget to replace `<node-ip>` with the IP address of the node where the web service is running.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

- [Mathesh M](https://www.linkedin.com/in/mathesh-me/) on LinkedIn.
- **Email:** itzmathesh@gmail.com

**Contributions are always welcome! Please create a PR to contribute to this project.**