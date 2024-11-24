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
    helm install my-jenkins-app . -n app
    ```

2. **Check status**:
    To check the status of the deployed WordPress release, run:

    ```sh
    helm status my-jenkins-app -n app
    ```

    Additionally, you can verify the Kubernetes resources:

    ```sh
    kubectl get all -l app=my-jenkins-app
    ```
    To view the logs of the WordPress and MariaDB pods:

    - **Get logs for the WordPress pod**:

      ```sh
      kubectl logs <wordpress-pod-name>
      ```

To uninstall/delete the `my-jenkins-app` deployment:

```sh
helm uninstall my-jenkins-app
