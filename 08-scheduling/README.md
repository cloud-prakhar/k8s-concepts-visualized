# Scheduling

> Status: Outline ready — detailed concept files coming soon.

## What You'll Learn

How Kubernetes decides which node runs which pod — and how to influence those decisions.

---

## How Scheduling Works (Recap)

```
New Pod (no node assigned)
        │
        ▼
Scheduler filters eligible nodes
        │
        ▼
Scheduler scores remaining nodes
        │
        ▼
Pod assigned to highest-scoring node
        │
        ▼
kubelet on that node runs the pod
```

---

## Topics in This Section

### 1. Resource Requests & Limits
- **Request:** Minimum resources the pod needs (scheduler uses this)
- **Limit:** Maximum resources the pod can use
- Scheduler only places pods on nodes with enough allocatable resources to meet requests

### 2. Node Selectors
- Simple label-based pod-to-node assignment
- `nodeSelector: disktype=ssd` → only schedule on nodes labeled `disktype=ssd`
- Rigid: no match = pod stays unscheduled

### 3. Node Affinity
- Richer version of nodeSelector
- `requiredDuringScheduling` — hard rule (like nodeSelector)
- `preferredDuringScheduling` — soft preference (scheduler tries but won't block)

### 4. Pod Affinity / Anti-Affinity
- **Affinity:** Schedule this pod near pods with label X (co-location)
- **Anti-Affinity:** Schedule this pod away from pods with label X (spread)
- Example: "Spread my 3 web replicas across 3 different nodes for HA"

### 5. Taints and Tolerations
- **Taint:** A mark on a node that repels pods
- **Toleration:** A permission on a pod to ignore a specific taint
- Example: GPU nodes are tainted — only ML pods with the toleration can run there

### 6. Priority and Preemption
- High-priority pods can evict lower-priority pods when resources are scarce
- PriorityClass defines priority levels

---

## Key Analogy

Scheduling is like **seating at an event**:
- **nodeSelector** = "I only want to sit in the front row" (rigid preference)
- **Affinity** = "I'd prefer to sit near my colleagues, but anywhere is fine" (soft preference)
- **Taint** = "This row is reserved — general admission not allowed"
- **Toleration** = "I have a VIP pass for the reserved row"
- **Anti-Affinity** = "Spread our team across different rows so one emergency doesn't affect everyone"

---

## Coming Soon

- `resource-requests-limits.md` — Sizing pods correctly
- `node-selectors-affinity.md` — Controlling node assignment
- `taints-tolerations.md` — Node reservation patterns
- `pod-affinity.md` — Co-location and spread strategies

---

## References

- [Assigning Pods to Nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)
- [Taints and Tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)
- [Pod Priority and Preemption](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)
