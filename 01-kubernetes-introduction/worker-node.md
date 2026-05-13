# Worker Nodes

## What is it?

A worker node is a machine (physical or virtual) in a Kubernetes cluster that runs containerized workloads (pods). Each worker node runs three key components: **kubelet** (node agent), **kube-proxy** (network rules), and a **container runtime** (actually runs containers).

---

## In Simple Language

Worker nodes are where your apps actually live and run.

The control plane is the brain — it makes decisions. Worker nodes are the body — they do the actual work. Every pod you deploy runs inside a container on a worker node.

A cluster typically has many worker nodes spread across physical machines or cloud VMs.

---

## Real World Analogy

A worker node is like a **factory floor** in a manufacturing plant:

| Factory | Worker Node |
|---------|-------------|
| Factory floor | Worker Node |
| Floor supervisor | kubelet |
| Internal mailroom | kube-proxy |
| Manufacturing machines | Container Runtime |
| Products being made | Containers (inside pods) |
| Work order from HQ | Instructions from API Server |

Factory HQ (control plane) sends work orders. The floor supervisor (kubelet) receives them, assigns tasks to machines (container runtime), and reports back to HQ on status. The mailroom (kube-proxy) ensures internal deliveries reach the right machine.

---

## Why This Exists

Worker nodes provide:
- **Isolation:** Workloads can be separated across nodes by team, app, or environment
- **Scalability:** Add more nodes to handle more workloads
- **Resilience:** If one node fails, the control plane reschedules its pods to other nodes
- **Heterogeneity:** Different node types can serve different needs (GPU nodes for ML, high-memory nodes for databases)

---

## How It Works

### kubelet

The kubelet is the primary node agent — it runs on every worker node.

1. Registers the node with the API Server
2. Watches the API Server for pods assigned to this node
3. Instructs the container runtime to start/stop containers
4. Reports node and pod health back to the API Server
5. Manages volumes and mounts for pods

```
API Server: "Run Pod X on this node"
    │
    ▼
kubelet receives the pod spec
    │
    ▼
kubelet asks container runtime: "Start these containers"
    │
    ▼
Container runtime pulls image, starts container
    │
    ▼
kubelet watches it, reports status to API Server
```

### kube-proxy

- Runs on every node as a network proxy
- Implements the Kubernetes Service concept — maintains network rules that allow pod-to-service communication
- Uses iptables (or IPVS) to route traffic to the correct pod IPs

```
Request to Service IP → kube-proxy rules → routed to one of the backend pod IPs
```

### Container Runtime

- The software that actually pulls images and runs containers
- Kubernetes talks to it via the Container Runtime Interface (CRI)
- Common runtimes: **containerd** (default in most modern K8s), **CRI-O**, Docker Engine

---

## Visual Diagram

**Worker Node Internals:**
```
┌────────────────────────────────────────────────┐
│                  Worker Node                   │
│                                                │
│  ┌────────────────────────────────────────┐    │
│  │              kubelet                   │    │
│  │  (watches API Server, manages pods)    │    │
│  └──────────────────┬─────────────────────┘    │
│                     │ instructs                │
│  ┌──────────────────┼──────────────────────┐   │
│  │      Container Runtime (containerd)     │   │
│  └──────────────────┬──────────────────────┘   │
│                     │ runs                     │
│         ┌───────────┴───────────┐              │
│         ▼                       ▼              │
│   ┌─────────────┐       ┌─────────────┐        │
│   │    Pod A    │       │    Pod B    │        │
│   │ [Container] │       │[Container 1]│        │
│   │             │       │[Container 2]│        │
│   └─────────────┘       └─────────────┘        │
│                                                │
│  ┌────────────────────────────────────────┐    │
│  │   kube-proxy (network routing rules)   │    │
│  └────────────────────────────────────────┘    │
└────────────────────────────────────────────────┘
         ▲ ▲
         │ │
   API Server communicates here
```

**Analogy Diagram:**
```
[HQ / Control Plane]
         │
         │ "Work order: build 3 units of Product X"
         ▼
[Factory Floor: Worker Node]
  [Floor Supervisor: kubelet] ──► [Machines: Container Runtime]
  [Mailroom: kube-proxy]                    │
                                      [Products: Pods]
```

> **Excalidraw idea:** A detailed factory floor view. Supervisor's desk (kubelet) near the entrance with a "received orders" inbox connected to a direct phone to HQ. Assembly machines (container runtime) in the middle running products (containers). A mailroom in the corner (kube-proxy) with routing tables on the wall. Loading docks connecting to other factory floors (inter-node networking).

---

## Key Terminologies

| Term | Technical Definition | Simple Explanation |
|------|---------------------|-------------------|
| **Worker Node** | A machine running containerized workloads in a cluster | A server where your apps actually run |
| **kubelet** | Node agent that manages pod lifecycle | The local supervisor on each node |
| **kube-proxy** | Network proxy managing service routing rules | The node's internal traffic router |
| **Container Runtime** | Software that runs containers (containerd, CRI-O) | The machine that actually runs your containers |
| **CRI** | Container Runtime Interface — K8s-to-runtime API | The standardized plug-in spec for container runtimes |
| **Node Capacity** | Total CPU/memory available on a node | The factory floor's total production capacity |
| **Node Allocatable** | Capacity available for pods (after system overhead) | Capacity minus what the OS and K8s system need |
| **Taint** | A mark on a node that repels certain pods | A "no entry" sign for pods that don't tolerate it |

---

## Node States

| State | Meaning |
|-------|---------|
| **Ready** | Node is healthy and accepting pods |
| **NotReady** | Node has a problem — control plane won't schedule pods here |
| **SchedulingDisabled** | Node is cordoned — existing pods stay, no new ones scheduled |
| **Unknown** | Control plane lost contact with the node |

---

## Common Misconceptions

- **"All nodes are identical"** — Nodes can have different hardware profiles. GPU nodes, high-memory nodes, and spot instances can all coexist in a cluster.
- **"kubelet is part of the control plane"** — kubelet runs on worker nodes, not the control plane. It's the agent that bridges the two.
- **"A node failure means pods are lost"** — The control plane detects the failure and reschedules pods on other nodes (assuming resources are available).
- **"kube-proxy handles all networking"** — kube-proxy handles Service routing rules. Pod-to-pod communication uses the CNI plugin (Calico, Flannel, etc.), not kube-proxy.

---

## Related Concepts

- [Control Plane](./control-plane.md)
- [Kubernetes Architecture](./kubernetes-architecture.md)
- [Pods](../02-core-objects/pods/README.md) (what runs on nodes)
- [Scheduling](../08-scheduling/README.md) (how pods are assigned to nodes)

---

## Additional Learning Resources

- [Node Components — Official Docs](https://kubernetes.io/docs/concepts/overview/components/#node-components)
- [kubelet — Official Reference](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/)
- [Container Runtime Interface](https://kubernetes.io/docs/concepts/architecture/cri/)
