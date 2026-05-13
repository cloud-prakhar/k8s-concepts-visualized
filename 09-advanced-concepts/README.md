# Advanced Concepts

> Status: Outline ready — detailed concept files coming soon.

## What You'll Learn

Higher-level abstractions and ecosystem tools built on top of core Kubernetes.

---

## Topics in This Section

### 1. Helm
- The package manager for Kubernetes
- **Charts** = reusable, configurable application templates
- Deploy complex apps (Redis, Prometheus, cert-manager) with a single command
- Manages releases, upgrades, and rollbacks of chart deployments

### 2. Custom Resource Definitions (CRDs)
- Extend the Kubernetes API with your own resource types
- Example: `kind: Database` or `kind: Certificate`
- The foundation of the Operator pattern

### 3. Operators
- Kubernetes-native applications that manage other applications
- Encode operational knowledge into software
- Use CRDs + controllers to manage complex stateful services (Postgres, Kafka, Elasticsearch)
- Example: "Create a PostgresCluster object → Operator sets up primary, replicas, backups automatically"

### 4. Jobs & CronJobs
- **Job** — A pod that runs to completion (batch processing, migrations)
- **CronJob** — A Job on a schedule (backups, reports, cleanup tasks)

### 5. DaemonSets
- Ensures one pod runs on every (or selected) node
- Use cases: log collectors, monitoring agents, network plugins
- When a new node joins, a DaemonSet pod is automatically created on it

### 6. StatefulSets
- For stateful applications needing stable identity and storage
- Each pod gets: stable DNS name, stable storage, ordered start/stop
- Use for: databases, Kafka, Zookeeper, Elasticsearch

### 7. GitOps
- Managing Kubernetes configuration via Git as the source of truth
- Changes to the cluster are made via Git commits, not kubectl
- Tools: Argo CD, Flux
- Git PR = cluster change request

---

## Key Analogy

Advanced Kubernetes concepts are like **management layers in a city**:

- **Helm** = The IKEA furniture catalog — pre-designed packages you assemble with a few steps
- **CRDs** = Inventing new types of permits the city can issue (beyond the standard ones)
- **Operators** = Specialists who know everything about one type of building (database buildings) and manage them autonomously
- **GitOps** = All city changes must go through the official planning office (Git) with a paper trail — no ad-hoc construction

---

## Coming Soon

- `helm.md` — Kubernetes package management
- `crds.md` — Extending the Kubernetes API
- `operators.md` — The Operator pattern
- `jobs-cronjobs.md` — Batch and scheduled workloads
- `daemonsets.md` — Node-level agents
- `statefulsets.md` — Stateful workloads
- `gitops.md` — Git-driven cluster management

---

## References

- [Helm](https://helm.sh/docs/)
- [Custom Resources — Official Docs](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)
- [Operator Pattern](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/)
- [Argo CD](https://argo-cd.readthedocs.io/)
- [Flux](https://fluxcd.io/docs/)
