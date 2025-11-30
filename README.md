Deployement Manifest: Explanation
Components Explained

[1]apiVersion: apps/v1
Kubernetes API version used for Deployments.

[2]kind: Deployment
Declares the resource type. Deployment manages pods and ReplicaSets.

[3]metadata
name → Deployment name (weather-app)
namespace → Namespace (weather)
labels → Key-value pairs to identify and organize resources

[4]spec
Defines the desired state of the Deployment.

replicas
Number of pods you want running (here 1).

selector
How Deployment finds which pods it manages. Must match pod template labels.

template
Pod template used to create pods.

metadata.labels → Must match selector labels.

spec.containers → Defines containers inside the pod.
containers
name → Container name
image → Docker image to run
ports → Container port (8080)
envFrom → Inject environment variables from ConfigMaps & Secrets


Components Explained:
[1] apiVersion:

| Resource Type         | API Group         | apiVersion           |
| --------------------- | ----------------- | -------------------- |
| Pod                   | core              | v1                   |
| Service               | core              | v1                   |
| ConfigMap             | core              | v1                   |
| Secret                | core              | v1                   |
| Namespace             | core              | v1                   |
| Node                  | core              | v1                   |
| Deployment            | apps              | apps/v1              |
| StatefulSet           | apps              | apps/v1              |
| DaemonSet             | apps              | apps/v1              |
| ReplicaSet            | apps              | apps/v1              |
| Job                   | batch             | batch/v1             |
| CronJob               | batch             | batch/v1             |
| Ingress               | networking.k8s.io | networking.k8s.io/v1 |
| NetworkPolicy         | networking.k8s.io | networking.k8s.io/v1 |
| PersistentVolume      | core              | v1                   |
| PersistentVolumeClaim | core              | v1                   |

[2] Kind:

| Kind                              | Description                                                                            |
| --------------------------------- | -------------------------------------------------------------------------------------- |
| **Pod**                           | The basic unit of deployment, can have one or more containers.                         |
| **Deployment**                    | Declarative updates for Pods; manages replica sets and rolling updates.                |
| **StatefulSet**                   | For stateful apps; ensures stable network IDs and persistent storage.                  |
| **DaemonSet**                     | Ensures a copy of a Pod runs on all (or selected) nodes.                               |
| **ReplicaSet**                    | Ensures a specified number of Pod replicas are running. Usually managed by Deployment. |
| **Service**                       | Exposes Pods as a network service inside or outside the cluster.                       |
| **ConfigMap**                     | Stores configuration data as key-value pairs.                                          |
| **Secret**                        | Stores sensitive data (passwords, keys, tokens).                                       |
| **Job**                           | Runs a Pod to completion (one-time tasks).                                             |
| **CronJob**                       | Runs Jobs on a schedule.                                                               |
| **Ingress**                       | Manages external HTTP/S access to Services.                                            |
| **PersistentVolume**              | Represents storage in the cluster.                                                     |
| **PersistentVolumeClaim**         | Requests storage from a PersistentVolume.                                              |
| **Namespace**                     | Logical partition of cluster resources.                                                |
| **NetworkPolicy**                 | Controls traffic flow between Pods.                                                    |
| **HorizontalPodAutoscaler (HPA)** | Automatically scales Pods based on metrics like CPU usage.                             |


[3] Key fields under metadata:

| Field                 | Purpose                                                                                                              |
| --------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **name**              | Unique name of the resource within a namespace. Mandatory.                                                           |
| **namespace**         | Logical grouping; defaults to `default` if not specified.                                                            |
| **labels**            | Key-value pairs used to organize, select,and filter resources.For example,a Deployment uses labels to match Pods. |



[4] Key fields in a Deployment spec

| Field        | Purpose                                                                      |
| ------------ | ---------------------------------------------------------------------------- |
| **replicas** | Number of desired Pod copies. Kubernetes ensures this many Pods are running. |
| **selector** | Label selector to match the Pods this Deployment manages.                    |
| **template** | Pod template that describes **what each Pod should look like**.              |
| **strategy** | How updates should be applied (RollingUpdate or Recreate).                   |

Inside template.spec (the Pod spec):

| Field                       | Purpose                                                                              |
| --------------------------- | ------------------------------------------------------------------------------------ |
| **containers**              | List of containers to run in the Pod. Each has `name`, `image`, `ports`, `env`, etc. |
| **volumes**                 | Define storage volumes to mount in the Pod.                                          |
| **nodeSelector / affinity** | Control which nodes Pods are scheduled on.                                           |
| **resources**               | CPU/memory requests and limits.                                                      |
| **restartPolicy**           | Pod restart behavior (`Always`, `OnFailure`, `Never`).                               |


-------------------------------------------------service.yml------------------------------------------------------------


Components Explained

[1]apiVersion: v1
Core Kubernetes API version used for Services.

[2]kind: Service
Declares this resource as a Service.

[3]metadata
name → Service name (weather-service)
namespace → Namespace (weather)

[4]spec
Desired state of the Service.

selector
Chooses the pods to send traffic to (matches app: weather-app).

ports
port → ClusterIP / Service port (80)
targetPort → Pod/container port where app is running (8080)

type
NodePort → Exposes the Service externally via <NodeIP>:<NodePort>

