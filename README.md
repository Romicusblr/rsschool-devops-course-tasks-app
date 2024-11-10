# Custom WordPress Helm Chart

This Helm chart deploys a WordPress site with a MariaDB database on a Kubernetes cluster.

## Prerequisites

- Kubernetes cluster (Minikube, GKE, EKS, etc.)
- Helm 3.x installed
- kubectl installed

## Installation

1. **Update `values.yaml`**:

    Edit the `values.yaml` file to configure your WordPress and MariaDB settings. Ensure the `service.type` is set to `NodePort` if you want to expose the service as a NodePort.

    ```yaml
    service:
      type: NodePort
      port: 80
      nodePort: 32000
    ```

2. **Deploy the Helm chart**:

    ```sh
    helm install wordpress .
    ```

2. **Check status**:
    To check the status of the deployed WordPress release, run:

    ```sh
    helm status wordpress
    ```

    Additionally, you can verify the Kubernetes resources:

    ```sh
    kubectl get all -l app=wordpress
    ```
    To view the logs of the WordPress and MariaDB pods:

    - **Get logs for the WordPress pod**:

      ```sh
      kubectl logs <wordpress-pod-name>
      ```

    - **Get logs for the MariaDB pod**:

      ```sh
      kubectl logs <mariadb-pod-name>
      ```

## Configuration

The following table lists the configurable parameters of the WordPress chart and their default values.

| Parameter                         | Description                                     | Default                        |
|-----------------------------------|-------------------------------------------------|--------------------------------|
| `replicaCount`                    | Number of WordPress replicas                    | `1`                            |
| `image.repository`                | WordPress image repository                      | `wordpress`                    |
| `image.tag`                       | WordPress image tag                             | `latest`                       |
| `image.pullPolicy`                | Image pull policy                               | `IfNotPresent`                 |
| `mariadb.enabled`                 | Enable MariaDB                                  | `true`                         |
| `mariadb.persistence.enabled`     | Enable MariaDB persistence                      | `true`                         |
| `mariadb.persistence.storageClass`| MariaDB storage class                           | `standard`                     |
| `mariadb.persistence.accessMode`  | MariaDB access mode                             | `ReadWriteOnce`                |
| `mariadb.persistence.size`        | MariaDB storage size                            | `1Gi`                          |
| `mariadb.db.name`                 | MariaDB database name                           | `wordpress`                    |
| `mariadb.db.user`                 | MariaDB database user                           | `wordpress`                    |
| `mariadb.db.password`             | MariaDB database password                       | `wordpress_password`           |
| `mariadb.db.rootPassword`         | MariaDB root password                           | `root_password`                |
| `service.type`                    | Kubernetes service type                         | `NodePort`                     |
| `service.port`                    | Kubernetes service port                         | `80`                           |
| `service.nodePort`                | Kubernetes node port                            | `30080`                        |

## Uninstallation

To uninstall/delete the `my-wordpress` deployment:

```sh
helm uninstall my-wordpress
