# Kubernetes (kubectl) Commands

This README provides a comprehensive list of common kubectl commands for managing Kubernetes clusters.

## Basic Commands

| Command | Description |
|---------|-------------|
| `kubectl version` | Display the Kubernetes version |
| `kubectl cluster-info` | Display cluster information |
| `kubectl get nodes` | List all nodes in the cluster |
| `kubectl get pods` | List all pods in the default namespace |
| `kubectl get pods --all-namespaces` | List all pods in all namespaces |
| `kubectl get services` | List all services in the default namespace |
| `kubectl get deployments` | List all deployments in the default namespace |
| `kubectl describe pod <pod_name>` | Show detailed information about a specific pod |
| `kubectl logs <pod_name>` | Fetch the logs of a specific pod |
| `kubectl exec -it <pod_name> -- /bin/bash` | Execute a command in a container (interactive shell) |

## Namespace Commands

| Command | Description |
|---------|-------------|
| `kubectl get namespaces` | List all namespaces |
| `kubectl create namespace <namespace_name>` | Create a new namespace |
| `kubectl delete namespace <namespace_name>` | Delete a namespace |

## Pod Management

| Command | Description |
|---------|-------------|
| `kubectl run <pod_name> --image=<image_name>` | Create a new pod with a specific image |
| `kubectl delete pod <pod_name>` | Delete a specific pod |
| `kubectl scale --replicas=<num> deployment/<deployment_name>` | Scale a deployment to a specified number of replicas |
| `kubectl rollout status deployment/<deployment_name>` | Show the rollout status of a deployment |
| `kubectl rollout undo deployment/<deployment_name>` | Roll back a deployment to a previous revision |
| `kubectl run static-busybox --image=busybox --restart=Never --dry-run=client -o yaml --command -- sleep 1000 > static-busy.yaml` | Create a pod as a static pod in /etc/kubernetes/manifests |

## Service Management

| Command | Description |
|---------|-------------|
| `kubectl expose deployment <deployment_name> --type=<service_type> --port=<port>` | Expose a deployment as a service |
| `kubectl get svc` | List all services |
| `kubectl delete svc <service_name>` | Delete a specific service |

## Deployment Management

| Command | Description |
|---------|-------------|
| `kubectl create -f <filename>` | Create resources from a file |
| `kubectl apply -f <filename>` | Apply changes to resources from a file |
| `kubectl delete -f <filename>` | Delete resources defined in a file |
| `kubectl set image deployment/<deployment_name> <container_name>=<new_image>` | Update the image of a deployment's container |

## ConfigMap and Secret Management

| Command | Description |
|---------|-------------|
| `kubectl create configmap <config_name> --from-literal=<key>=<value>` | Create a ConfigMap from literal values |
| `kubectl get configmaps` | List all ConfigMaps |
| `kubectl delete configmap <config_name>` | Delete a specific ConfigMap |
| `kubectl create secret generic <secret_name> --from-literal=<key>=<value>` | Create a Secret from literal values |
| `kubectl get secrets` | List all secrets |
| `kubectl delete secret <secret_name>` | Delete a specific secret |

## Persistent Volumes (PV) and Persistent Volume Claims (PVC)

| Command | Description |
|---------|-------------|
| `kubectl get pv` | List all persistent volumes |
| `kubectl get pvc` | List all persistent volume claims |
| `kubectl create -f <pv.yaml>` | Create a persistent volume from a file |
| `kubectl create -f <pvc.yaml>` | Create a persistent volume claim from a file |
| `kubectl delete pv <pv_name>` | Delete a specific persistent volume |
| `kubectl delete pvc <pvc_name>` | Delete a specific persistent volume claim |

## RBAC (Role-Based Access Control)

| Command | Description |
|---------|-------------|
| `kubectl get roles` | List all roles |
| `kubectl get rolebindings` | List all role bindings |
| `kubectl create role <role_name> --verb=<verb> --resource=<resource>` | Create a new role |
| `kubectl create rolebinding <binding_name> --role=<role_name> --user=<user_name>` | Bind a role to a user |
| `kubectl delete role <role_name>` | Delete a specific role |
| `kubectl delete rolebinding <binding_name>` | Delete a specific role binding |

## Additional Useful Commands

| Command | Description |
|---------|-------------|
| `kubectl top nodes` | Display resource usage of nodes |
| `kubectl top pods` | Display resource usage of pods |
| `kubectl edit <resource_type> <resource_name>` | Edit a resource on the server |
| `kubectl label <resource_type> <resource_name> <label_key>=<label_value>` | Add or update a label on a
