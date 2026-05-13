# Namespaces

## What is it?

Kubernetes Namespaces are virtual clusters within a physical cluster. They provide a mechanism to divide cluster resources between multiple users, teams, or environments using resource isolation, access control, and resource quotas — all within a single cluster.

---

## In Simple Language

A Namespace is a way to split one Kubernetes cluster into multiple virtual sections.

Imagine having one big building but dividing it into separate floors for different teams — each floor has its own rules, its own people, and its own stuff. But it's still the same physical building.

---

## Real World Analogy

Namespaces are like **floors in an office building**:

- The **building** = the Kubernetes cluster
- Each **floor** = a Namespace (e.g., `dev`, `staging`, `production`)
- **Offices on each floor** = pods and services
- Floor residents (teams) can't casually wander into other floors
- Building management (cluster admin) can access all floors
- Each floor can have its own rules and budget (resource quotas)

The marketing team on Floor 3 doesn't know what engineering is doing on Floor 7 — and that's fine. They're in the same building but logically separated.

---

## Why This Exists

A single Kubernetes cluster is shared infrastructure. Without Namespaces:
- All teams would share one flat resource pool
- Resources could conflict (e.g., two teams both try to name a service "web")
- No way to apply per-team access control
- No way to limit resource usage per team

Namespaces solve:
- **Name isolation:** Two teams can have a service named "web" in different namespaces
- **Access control:** RBAC policies can be scoped per namespace
- **Resource quotas:** Limit CPU/memory per namespace per team
- **Environment separation:** `dev`, `staging`, `production` in one cluster

---

## How It Works

1. Namespace is created as a Kubernetes object
2. Resources (pods, services, secrets, configmaps) are created inside a namespace
3. Names only need to be unique within a namespace
4. Some resources are cluster-scoped (not namespaced): Nodes, PersistentVolumes, ClusterRoles

**Default namespaces in every cluster:**

| Namespace | Purpose |
|-----------|---------|
| `default` | Where resources go if you don't specify a namespace |
| `kube-system` | Kubernetes system components (API Server, CoreDNS, etc.) |
| `kube-public` | Publicly readable data, rarely used |
| `kube-node-lease` | Node heartbeat objects |

**Cross-namespace communication:**
Pods in different namespaces can still communicate using the full DNS name:
```
http://my-service.other-namespace.svc.cluster.local
```

---

## Visual Diagram

**Namespaces as Floors:**
```
┌─────────────────────────────────────────────────────┐
│                Kubernetes Cluster                   │
│                                                     │
│  ┌───────────────────┐   ┌───────────────────────┐  │
│  │  Namespace: dev   │   │ Namespace: production │  │
│  │  [Pod: web]       │   │ [Pod: web]            │  │
│  │  [Pod: api]       │   │ [Pod: api]            │  │
│  │  [Svc: web]       │   │ [Svc: web]            │  │
│  │  Quota: 4 CPU     │   │ Quota: 32 CPU         │  │
│  └───────────────────┘   └───────────────────────┘  │
│                                                     │
│  ┌──────────────────────────────────────────────┐   │
│  │          Namespace: kube-system              │   │
│  │  [CoreDNS] [kube-proxy] [API Server Pods]    │   │
│  └──────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
```

> **Excalidraw idea:** Building cross-section showing 3 floors. Floor 1 labeled "dev" — small team, less furniture (fewer resources). Floor 2 labeled "production" — larger team, more resources. Basement labeled "kube-system." Elevator shaft in the middle with "Admin access to all floors." Small lock icons on each floor entrance representing RBAC.

---

## Key Terminologies

| Term | Technical Definition | Simple Explanation |
|------|---------------------|-------------------|
| **Namespace** | A virtual cluster providing resource isolation | A logical division/floor within the cluster |
| **Resource Quota** | Limits on total resource usage within a namespace | The budget cap for each floor |
| **LimitRange** | Default and max resource limits per pod in a namespace | Standard room size rules per floor |
| **RBAC** | Role-Based Access Control — who can do what | The access badge system per floor |
| **kube-system** | Built-in namespace for Kubernetes system components | The building's mechanical room |
| **Cluster-scoped resources** | Resources not bound to any namespace (Nodes, PVs) | Building-wide infrastructure, not per-floor |

---

## Common Misconceptions

- **"Namespaces provide strong isolation"** — Namespaces provide logical, not physical, isolation. Pods in different namespaces still run on the same nodes and share network hardware. Use NetworkPolicies for network isolation.
- **"I should always create many namespaces"** — Don't over-namespace. Start with `dev`, `staging`, `production`. Add per-team namespaces only when you have genuine isolation needs.
- **"The default namespace is fine forever"** — As your cluster grows, using only `default` becomes messy. Introduce namespace organization early.
- **"Namespaces separate networks"** — Not by default. You need NetworkPolicies to restrict cross-namespace pod communication.

---

## Related Concepts

- [Labels & Selectors](../labels-selectors/README.md) — Another way to organize resources
- [Security / RBAC](../../05-security/README.md) — Namespace-scoped access control
- [Resource Quotas — Official Docs](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

---

## Additional Learning Resources

- [Namespaces — Official Docs](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)
- [Share a Cluster with Namespaces](https://kubernetes.io/docs/tasks/administer-cluster/namespaces/)
- [Resource Quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/)
