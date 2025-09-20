# Kubernetes System ⛵

Kubernetes is an open-source platform for automating deployment, scaling, and management of containerized applications.

## Key Features
- Automatically replaces crashed containers
- Scales containers based on traffic
- Distributes traffic with load balancing
- Provides monitoring and CRUD operations for pods
- Works with any cloud provider
- Similar to Docker Compose, but for multiple machines

> **Note:** Kubernetes manages containers, not infrastructure. For infrastructure management, use IaC tools like [Terraform](https://www.notion.so/Terraform-23f5b34e9f5080b7a119c8f9213cbdba?pvs=21).

## Core Concepts

#### Pod
- Smallest deployable unit
- Runs inside a worker node with cluster-internal IP
- Can contain multiple containers sharing resources

#### Deployment (Controller)
- Manages pods: create, move, pause, delete, roll back
- Defines scaling policies

#### Service
- Exposes pods within the cluster or externally
- Groups pods with shared *unchangeable* IP
- allows external access to Pods

#### Proxy
- Manages network traffic for worker nodes

#### Worker Node
- Like a machine or VM
- Hosts multiple pods and proxies

#### Master Node
- Coordinates worker nodes
- Typically runs on a separate machine


# Kubernetes Deployments

#### Get info

`kubectl get deployments`

`kubectl get pods`

`kubectl get services`

#### Manage obj

`kubectl create deployment <name> --image=<image>`

`kubectl expose deployment <name> --type=NodePort --port=<port>`

`kubectl scale deployment/<name> --replicas=5`

Update deployment with new image
`kubectl set image deployment/<name> <container-name>=<new-iamge>:<tag>`

Monitor progress/status of deployment rollout
`kubectl rollout status deployment/<deployment-name>`

Rollout history with --revision
`kubectl rollout history deployment/<deployment-name>`

Rollback deployment with --to-revision
`kubectl rollout undo deployment/<deployment-name>`


### Delete obj
`kubectl delete deployment <name>`

`kubectl delete service <name>`


## How It Works
1. Deployment object is created and sent to the cluster.
2. Scheduler selects the best node for the new pod.
3. Pod is created on the node.
4. Kubelet monitors pod health.
5. Pod runs the specified container image.

## Notes
- Clusters cannot access local Docker images directly.
- Pods run on worker nodes with local IPs; use a Service object to access them.


## Deploy declaratively
`kubectl apply -f=deployment.yaml`
`kebectl delete -f=deployment.yaml`