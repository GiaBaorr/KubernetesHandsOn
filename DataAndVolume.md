# STATE
State is data created and used by applications:
* User generated (databases, files, etc.)
* Intermediate results (cache, temporary databases)

Kubernetes acts as an **orchestrator** - it creates and runs pods & containers.
Containers don't run with docker-compose or docker run, so we can't use `-v` or volumes from Docker CLI.

→ We must configure Kubernetes to handle persistent data.

## Volume
Volumes are part of pods and provide storage that can be shared between containers in the same pod.

**Volume lifetime**: Volumes survive container restarts/recreation but are destroyed when the pod is deleted.

Define/config volume together with define/config pod

| Kubernetes | Docker |
|------------|--------|
| Many volume types: emptyDir, hostPath, configMap, secret, persistentVolumeClaim, cloud storage (AWS EBS, GCP PD, etc.) | Limited types: named volumes, bind mounts, tmpfs |
| Survives container restarts, **not pod deletion** | Survives container removal until explicitly deleted |
| Integrated with cloud providers and storage systems | Primarily local host storage |


### Types
- emptyDir: create empty directory when pods start, keep it and fill data into

  **replicas** should be considered, 2 different pods -> 2 diferent directories -> use hostPath

- hostPath: mount file/dir into pods
  **exists for multi pods** but not for **multi working nodes**

- CSI: like interface that we can custom dynamically, build to adapt the requirement
  It is **driver interface to use PVs**

- Others: connect to amazon ebs, nfs - connect to file system, amazon elastic file...



## Persistent Volumes (PV) & Claims (PVC)
For data that needs to survive pod deletion:
* **PersistentVolume (PV)**: Cluster-level storage resource
* **PersistentVolumeClaim (PVC)**: Request for storage by a pod, placed inside working node