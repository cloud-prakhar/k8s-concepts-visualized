# Learning Path

A structured guide to understanding Kubernetes from scratch — no experience required.

Each stage builds on the previous. Don't skip stages.

---

## Stage 0 — Prerequisites (Start Here)

> Goal: Understand the building blocks Kubernetes is built on top of.

| # | Topic | Why It Matters |
|---|-------|---------------|
| 1 | [What is a Server?](../00-prerequisites/what-is-a-server.md) | Kubernetes manages servers — know what you're managing |
| 2 | [Virtualization vs Containers](../00-prerequisites/virtualization-vs-containers.md) | Understand what runs inside Kubernetes |
| 3 | [What is Docker?](../00-prerequisites/what-is-docker.md) | Kubernetes orchestrates Docker containers |
| 4 | [Networking Basics](../00-prerequisites/networking-basics.md) | K8s is a networked system — IPs, ports, DNS matter |
| 5 | [Why Orchestration?](../00-prerequisites/why-orchestration.md) | Understand the *problem* K8s solves |

---

## Stage 1 — Kubernetes Introduction

> Goal: Understand what Kubernetes is and how it's structured at a high level.

| # | Topic | Why It Matters |
|---|-------|---------------|
| 1 | [What is Kubernetes?](../01-kubernetes-introduction/what-is-kubernetes.md) | The big picture |
| 2 | [Kubernetes Architecture](../01-kubernetes-introduction/kubernetes-architecture.md) | The city map |
| 3 | [The Control Plane](../01-kubernetes-introduction/control-plane.md) | The brain of the cluster |
| 4 | [Worker Nodes](../01-kubernetes-introduction/worker-node.md) | Where your apps actually run |

---

## Stage 2 — Core Objects

> Goal: Understand the fundamental building blocks you'll work with every day.

| # | Topic | Why It Matters |
|---|-------|---------------|
| 1 | [Pods](../02-core-objects/pods/README.md) | The smallest deployable unit |
| 2 | [ReplicaSets](../02-core-objects/replicasets/README.md) | Keeping the right number of pods alive |
| 3 | [Deployments](../02-core-objects/deployments/README.md) | Managing and updating your apps |
| 4 | [Services](../02-core-objects/services/README.md) | Stable networking for ephemeral pods |
| 5 | [Namespaces](../02-core-objects/namespaces/README.md) | Logical separation within a cluster |
| 6 | [Labels & Selectors](../02-core-objects/labels-selectors/README.md) | Grouping and targeting resources |

---

## Stage 3 — Networking

> Goal: Understand how pods communicate inside and outside the cluster.

→ [03-networking](../03-networking/README.md)

---

## Stage 4 — Storage

> Goal: Understand how stateful apps handle persistent data.

→ [04-storage](../04-storage/README.md)

---

## Stage 5 — Security

> Goal: Understand who can do what in your cluster.

→ [05-security](../05-security/README.md)

---

## Stage 6 — Scaling

> Goal: Understand how Kubernetes grows and shrinks to meet demand.

→ [06-scaling](../06-scaling/README.md)

---

## Stage 7 — Observability

> Goal: Understand how to know what's happening in your cluster.

→ [07-observability](../07-observability/README.md)

---

## Stage 8 — Scheduling

> Goal: Understand how Kubernetes decides where to run workloads.

→ [08-scheduling](../08-scheduling/README.md)

---

## Stage 9 — Advanced Concepts

> Goal: Explore higher-level abstractions built on top of Kubernetes.

→ [09-advanced-concepts](../09-advanced-concepts/README.md)
