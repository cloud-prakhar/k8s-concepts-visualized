# The Control Plane

## What is it?

The Kubernetes control plane is the set of components that manage the overall state of the cluster. It makes all global decisions (scheduling, scaling, responding to failures) and exposes the Kubernetes API. It is the brain of a Kubernetes cluster.

Control plane components: **API Server, etcd, Scheduler, Controller Manager, Cloud Controller Manager**.

---

## In Simple Language

The control plane is Kubernetes headquarters.

It doesn't run your applications — it manages everything. It watches the cluster, makes decisions, and gives instructions to worker nodes. It's always asking: "Is the cluster in the state I was told it should be? If not, fix it."

---

## Real World Analogy

Think of the control plane as **City Hall**:

| City Hall Room | Control Plane Component | Role |
|---------------|------------------------|------|
| Mayor's desk (front door) | API Server | All requests go here first |
| City archives vault | etcd | Official records of everything |
| Urban planning office | Scheduler | Decides where to place new pods |
| Department of maintenance | Controller Manager | Watches and fixes everything |
| Liaison office (cloud) | Cloud Controller Manager | Talks to AWS/GCP/Azure |

Citizens (you, kubectl) only talk to the Mayor's desk. They don't wander into the archives or planning office directly. City Hall internally coordinates everything.

---

## Why This Exists

The control plane exists to provide:
- **A single source of truth** (etcd) for all cluster state
- **Centralized decision making** (Scheduler, Controllers) rather than individual nodes making decisions
- **A unified API** (API Server) so all tools interact the same way
- **Automatic reconciliation** — continuously fixing drift between desired and actual state

Without a control plane, nodes would be isolated computers with no coordination.

---

## How It Works

### API Server (kube-apiserver)

- The front door to the cluster — all external and internal communication goes through it
- Validates and processes REST API requests
- Reads and writes to etcd
- Sends accepted changes to relevant components (Scheduler, kubelet, etc.)

```
kubectl apply -f deployment.yaml
    │
    ▼
API Server validates → authenticates → authorizes
    │
    ▼
Writes desired state to etcd
    │
    ▼
Notifies controllers and scheduler
```

### etcd

- Distributed, highly-available key-value store
- Stores all cluster state: nodes, pods, configs, secrets, roles, etc.
- Only the API Server talks directly to etcd
- If etcd goes down, the cluster can't make changes (but running pods keep running)

### Scheduler (kube-scheduler)

- Watches for newly created pods with no assigned node
- Scores each eligible node based on: resource availability, affinity rules, taints, etc.
- Assigns the pod to the best-scoring node
- Does NOT run the pod — just assigns it. The kubelet on that node runs it.

```
New Pod appears (no node assigned)
    │
    ▼
Scheduler finds eligible nodes
    │
    ▼
Scores each node (CPU, memory, affinity, etc.)
    │
    ▼
Picks the best node, updates pod's node field
    │
    ▼
kubelet on that node picks it up and runs it
```

### Controller Manager (kube-controller-manager)

- Runs multiple built-in controllers as a single process
- Each controller watches for changes and reconciles state

Key controllers:
| Controller | What it watches | What it does |
|-----------|----------------|--------------|
| Node Controller | Node health | Marks nodes as unavailable when they go down |
| Replication Controller | Pod counts | Ensures the desired number of pods run |
| Endpoints Controller | Services + Pods | Keeps Service endpoint lists up to date |
| Namespace Controller | Namespaces | Cleans up resources when namespaces are deleted |

### Cloud Controller Manager

- Optional component when running K8s on a cloud provider
- Manages cloud-specific resources: LoadBalancers, persistent disks, node lifecycle
- Keeps Kubernetes cloud-provider-independent by abstracting cloud APIs

---

## Visual Diagram

> **Interactive diagram:** Open [`control-plane.excalidraw`](../diagrams/control-plane.excalidraw) in VSCode with the **Excalidraw** extension.

**Control Plane Internal Flow:**
```
[kubectl apply -f pod.yaml]
         │
         ▼
┌─────────────────────────────────────────────────────┐
│                   Control Plane                     │
│                                                     │
│  ┌──────────────┐   write state   ┌──────────────┐  │
│  │  API Server  │◄───────────────►│    etcd      │  │
│  └──────┬───────┘                 └──────────────┘  │
│         │                                           │
│         │ notifies                                  │
│    ┌────┴────────────────────┐                      │
│    │                         │                      │
│    ▼                         ▼                      │
│ ┌──────────┐         ┌──────────────────┐           │
│ │Scheduler │         │ Controller Mgr   │           │
│ │"assign   │         │ "maintain state" │           │
│ │ to node" │         └──────────────────┘           │
│ └────┬─────┘                                        │
│      │ tells kubelet                                │
└──────┼──────────────────────────────────────────────┘
       │
       ▼
  [Node's kubelet] ──► runs the container
```

> **Excalidraw idea:** City Hall floorplan view. Front door labeled "API Server" with a clerk stamping requests. A vault room labeled "etcd" locked with only the clerk having a key. An urban planning room with a map of the city (Scheduler). A monitoring room with dashboards (Controllers). Only City Hall staff interact between rooms — citizens only see the front door.

---

## Key Terminologies

| Term | Technical Definition | Simple Explanation |
|------|---------------------|-------------------|
| **API Server** | RESTful frontend for Kubernetes; validates and routes all requests | The single entry point to the cluster |
| **etcd** | Distributed consistent key-value store for cluster data | The cluster's ledger — what is supposed to exist |
| **Scheduler** | Watches for unscheduled pods and assigns nodes | The city planner deciding where new pods live |
| **Controller Manager** | Hosts control loops maintaining desired state | The maintenance department fixing anything off-spec |
| **Control Loop** | A non-terminating loop that regulates state | Watch → compare → act → repeat |
| **Reconciliation** | The act of correcting drift from desired state | Fixing reality to match the plan |
| **Cloud Controller Manager** | Integrates Kubernetes with cloud provider APIs | The liaison that talks to AWS/GCP/Azure for you |

---

## Common Misconceptions

- **"The control plane runs on one machine"** — In production, control plane components run on multiple machines for high availability.
- **"I can run workloads on the control plane"** — You technically can, but it's strongly discouraged. Control plane nodes are dedicated to cluster management.
- **"etcd backs up automatically"** — You must configure etcd backups explicitly. Losing etcd without a backup is catastrophic.
- **"The Scheduler picks the fastest node"** — The Scheduler picks the most suitable node based on resource fit, constraints, and rules — not just speed.
- **"Controllers are slow to react"** — Controllers typically reconcile within seconds of a state change.

---

## Related Concepts

- [Worker Nodes](./worker-node.md)
- [Kubernetes Architecture](./kubernetes-architecture.md)
- [Pods](../02-core-objects/pods/README.md)
- [Deployments](../02-core-objects/deployments/README.md) (managed by controllers)

---

## Additional Learning Resources

- [Kubernetes Control Plane — Official Docs](https://kubernetes.io/docs/concepts/overview/components/#control-plane-components)
- [How the Kubernetes Scheduler Works](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)
- [Understanding etcd](https://etcd.io/docs/v3.5/learning/)
