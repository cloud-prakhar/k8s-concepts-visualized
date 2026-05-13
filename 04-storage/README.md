# Storage

> Status: Outline ready — detailed concept files coming soon.

## What You'll Learn

How Kubernetes handles persistent data in a world of ephemeral pods.

---

## The Core Problem

Containers are ephemeral. When a pod dies, all data written inside it is lost.

For stateful apps (databases, file stores), you need data that outlives the pod.

---

## Topics in This Section

### 1. Volumes
- Storage attached to a pod's lifecycle
- Dies with the pod (emptyDir) or survives it (hostPath, cloud volumes)
- Types: emptyDir, hostPath, configMap, secret, nfs, cloud provider volumes

### 2. PersistentVolume (PV)
- A piece of storage provisioned by an admin or dynamically
- Independent of any pod's lifecycle
- Exists in the cluster until explicitly deleted

### 3. PersistentVolumeClaim (PVC)
- A request for storage by a user/pod
- Binds to a matching PersistentVolume
- The pod uses the PVC — decoupled from where storage actually lives

### 4. StorageClass
- Defines types of storage available (SSD, HDD, network storage)
- Enables dynamic provisioning — PVs created on demand
- Examples: gp2 (AWS EBS), standard (GCP), managed-csi (Azure)

### 5. StatefulSets
- Workload controller for stateful apps
- Each pod gets a stable identity and stable storage
- Ordered deployment and scaling (pod-0 before pod-1)

---

## Key Analogy

Think of Kubernetes storage like a **locker system** at a gym:

- **Volume** = A temporary locker assigned to you for one gym visit (lost when you leave)
- **PersistentVolume** = A permanent locker maintained by the gym (survives your visit)
- **PVC** = Your locker rental request (size, access type)
- **StorageClass** = The type of locker (small, large, climate-controlled)

---

## Coming Soon

- `volumes.md` — Temporary and ephemeral storage
- `persistent-volumes.md` — PV and PVC deep dive
- `storage-classes.md` — Dynamic provisioning
- `statefulsets.md` — Running stateful applications

---

## References

- [Storage — Official Docs](https://kubernetes.io/docs/concepts/storage/)
- [Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
- [Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)
