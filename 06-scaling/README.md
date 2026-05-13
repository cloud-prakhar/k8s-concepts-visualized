# Scaling

> Status: Outline ready — detailed concept files coming soon.

## What You'll Learn

How Kubernetes automatically grows and shrinks your applications and the cluster itself to match demand.

---

## Three Dimensions of Scaling

| Dimension | What Scales | Controller |
|-----------|------------|-----------|
| **Horizontal Pod** | Number of pod replicas | HPA |
| **Vertical Pod** | CPU/memory of individual pods | VPA |
| **Cluster** | Number of nodes | Cluster Autoscaler |

---

## Topics in This Section

### 1. Horizontal Pod Autoscaler (HPA)
- Automatically scales the number of pod replicas based on metrics
- Common metrics: CPU utilization, memory, custom metrics
- "Traffic doubled → scale from 3 pods to 6 pods"

### 2. Vertical Pod Autoscaler (VPA)
- Automatically adjusts CPU/memory requests and limits for pods
- Useful when pod sizing is hard to predict
- Can conflict with HPA — use carefully

### 3. Cluster Autoscaler
- Adds or removes nodes from the cluster based on pending pods
- Works with cloud providers (AWS ASG, GCP MIG, Azure VMSS)
- "Pods can't be scheduled due to resource shortage → add a new node"

### 4. Manual Scaling
- `kubectl scale deployment my-app --replicas=10`
- Immediate but not automated

---

## Key Analogy

Kubernetes scaling is like a **conference center**:

- **HPA** = Booking more meeting rooms (pods) when more attendees arrive
- **VPA** = Upgrading a meeting room to a larger one (more CPU/RAM per pod)
- **Cluster Autoscaler** = Adding an entire new building wing (new node) when no more rooms are available

The smart conference center manager (K8s) handles all of this automatically based on current demand.

---

## Coming Soon

- `hpa.md` — Horizontal Pod Autoscaler deep dive
- `vpa.md` — Vertical Pod Autoscaler
- `cluster-autoscaler.md` — Adding/removing nodes
- `resource-requests-limits.md` — Foundation for autoscaling

---

## References

- [HPA — Official Docs](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)
- [VPA — GitHub](https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler)
- [Cluster Autoscaler](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler)
