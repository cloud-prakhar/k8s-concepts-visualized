# Labels & Selectors

## What is it?

**Labels** are key-value pairs attached to Kubernetes objects (pods, services, nodes, etc.) as metadata. **Selectors** are queries that filter and group objects based on their labels. Together, they form Kubernetes' primary mechanism for organizing and cross-referencing resources.

---

## In Simple Language

Labels are like **tags** you attach to things. Selectors are like **filters** that find things by their tags.

You put a label `app=web` on your pods. Then a Service uses a selector `app=web` to find those pods and route traffic to them. A ReplicaSet uses the same selector to know which pods it owns.

Labels are how Kubernetes resources talk to each other.

---

## Real World Analogy

Labels and Selectors work like a **music playlist system**:

- **Labels** = tags on songs (genre=rock, mood=energetic, artist=Queen)
- **Selector** = the filter ("show me all rock songs with high energy")
- **Result** = the playlist of matching songs

Spotify doesn't tell you "here are songs #1, #2, #7" — it says "here are all songs matching your criteria."

Kubernetes doesn't say "here are pods named pod-1, pod-2" — it says "here are all pods with label `app=web`."

Another analogy: **color-coded hospital wristbands**:
- Each patient (pod) has wristbands with info: dept=cardiology, risk=high, ward=4
- A nurse (Service) looking for all cardiology patients uses selector `dept=cardiology`
- An alert system (controller) looking for high-risk patients uses selector `risk=high`
- Same patients, different filters finding them for different purposes

---

## Why This Exists

Kubernetes has no hardcoded relationships between objects. A Service doesn't say "I serve Pod X and Pod Y by name." Instead, it says "I serve anything labeled `app=web`."

This design means:
- **Flexibility:** Labels and selectors work across any number of objects
- **Decoupling:** Services, ReplicaSets, and Deployments don't need to know pod names
- **Dynamic grouping:** As pods are created/deleted, selectors automatically include/exclude them
- **Multi-dimensional organization:** One pod can have many labels, grouped in different ways by different selectors

---

## How It Works

**Adding labels to a pod:**
Any Kubernetes object can have labels — they're just key-value pairs you define.

Examples of label keys and values:
```
app=web            environment=production
tier=frontend      version=v2
team=platform      region=us-east
```

**Using selectors:**
- **Equality-based:** `app=web` (exact match), `environment!=dev` (not equal)
- **Set-based:** `environment in (prod, staging)`, `tier notin (backend)`

**How resources use selectors:**

| Resource | Uses Selector For |
|----------|------------------|
| Service | Finding pods to route traffic to |
| ReplicaSet | Finding pods it "owns" |
| Deployment | Finding its ReplicaSets |
| NetworkPolicy | Selecting which pods the policy applies to |
| Node Affinity | Selecting which nodes to schedule on |

---

## Visual Diagram

**Labels on pods:**
```
Pod A                    Pod B                    Pod C
┌──────────────┐         ┌──────────────┐         ┌──────────────┐
│ app=web      │         │ app=web      │         │ app=api      │
│ env=prod     │         │ env=staging  │         │ env=prod     │
│ version=v2   │         │ version=v1   │         │ version=v1   │
└──────────────┘         └──────────────┘         └──────────────┘
```

**Selector queries:**
```
selector: app=web
  → matches Pod A, Pod B

selector: app=web, env=prod
  → matches Pod A only

selector: env=prod
  → matches Pod A, Pod C
```

**Service using selector to find pods:**
```
Service: web-prod-svc
  selector: {app: web, env: prod}
         │
         ├── finds Pod A ✓
         ├── skips Pod B (env=staging) ✗
         └── skips Pod C (app=api) ✗

Traffic routed only to Pod A
```

> **Excalidraw idea:** Three colored wristband-wearing figures (pods). Each has 2-3 wristband tags shown. A "selector filter" funnel in the center with different queries dropping in, and different subsets of figures coming out the other side. Show that the same figures appear in different results based on the query.

---

## Key Terminologies

| Term | Technical Definition | Simple Explanation |
|------|---------------------|-------------------|
| **Label** | A key-value pair attached to a Kubernetes object | A tag describing an object's attributes |
| **Selector** | A query that matches objects by their labels | A filter that finds objects by their tags |
| **Annotation** | Key-value pair for non-identifying metadata | Labels for humans/tools, not for K8s logic |
| **Equality-based selector** | Matches exact label key=value | "Give me everything tagged app=web" |
| **Set-based selector** | Matches label values within a set | "Give me anything in (prod, staging)" |
| **Label schema** | A team's naming convention for labels | The agreed-upon tagging system |

---

## Recommended Label Schema

A good label schema makes selectors predictable:

```
app:         web / api / worker / db
environment: dev / staging / production
version:     v1.2.0 / latest
tier:        frontend / backend / data
team:        platform / payments / auth
```

---

## Common Misconceptions

- **"Labels and annotations are the same"** — Labels are for Kubernetes to select/group objects. Annotations are metadata for humans and external tools — K8s doesn't use them for logic.
- **"Only pods have labels"** — Any Kubernetes object can have labels: nodes, services, namespaces, secrets, etc.
- **"Label selectors are slow"** — Label lookups are highly optimized in etcd. Selectors are fast at cluster scale.
- **"Two resources can't select the same pods"** — They can and often do. A Service and a NetworkPolicy might both select the same set of pods.

---

## Related Concepts

- [Pods](../pods/README.md) — What you label most often
- [Services](../services/README.md) — Use selectors to find pods
- [ReplicaSets](../replicasets/README.md) — Use selectors to own pods
- [Namespaces](../namespaces/README.md) — Another organization layer

---

## Additional Learning Resources

- [Labels and Selectors — Official Docs](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)
- [Recommended Labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/)
- [Annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/)
