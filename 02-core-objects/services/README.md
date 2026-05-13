# Services

## What is it?

A Kubernetes Service is an abstraction that defines a stable network endpoint for a set of pods. It provides a consistent IP address and DNS name that remains fixed even as pods are created, destroyed, or replaced. It load-balances traffic across all matching pods.

---

## In Simple Language

Pods are ephemeral — they come and go, and their IP addresses change every time they're replaced.

A Service gives you a **permanent address** that always routes traffic to the right pods, no matter how many times those pods restart or change.

It's the stable front door that the outside world (or other services) uses to reach your app.

---

## Real World Analogy

A Service is like a **company's main phone number**:

- The company's **public phone number** (Service IP/DNS) never changes
- Behind the scenes, calls get routed to **whichever employee is available** (load-balanced to pods)
- Employees (pods) come and go — people get hired, leave, take breaks
- But the phone number stays the same — callers never need to know which employee answers

Without a Service: you'd have to look up every individual employee's direct line and update it every time someone new starts.
With a Service: one number, always works, always reaches someone.

---

## Why This Exists

Pods have dynamic IPs that change when pods restart. Without Services:
- Other apps would need to track pod IPs constantly
- Load balancing across replicas would require external tools
- External traffic would have no stable entry point

Services solve:
- **Stable addressing:** Fixed ClusterIP and DNS name
- **Load balancing:** Traffic spread across all healthy pods
- **Decoupling:** Clients don't know about individual pods
- **Service discovery:** Other pods find services by DNS name, not IP

---

## How It Works

A Service uses **label selectors** to identify which pods it routes traffic to.

```
Service (app=web) ──► finds all pods with label app=web
                  ──► creates Endpoints list of their IPs
                  ──► kube-proxy routes traffic to those IPs
```

When a pod is added or removed:
1. The Endpoints controller updates the Service's endpoint list automatically
2. kube-proxy updates routing rules on every node
3. Traffic automatically flows to new pods, avoids dead ones

---

## Service Types

| Type | Accessibility | Use Case |
|------|--------------|---------|
| **ClusterIP** (default) | Inside cluster only | Internal service-to-service communication |
| **NodePort** | Via any Node's IP + port | Basic external access (dev/testing) |
| **LoadBalancer** | Via a cloud load balancer | Production external access on cloud |
| **ExternalName** | Maps to an external DNS name | Aliasing external services into the cluster |

---

## Visual Diagram

> **Interactive diagram:** Open [`service-types.excalidraw`](../../diagrams/service-types.excalidraw) in VSCode with the **Excalidraw** extension.

**Service as Stable Front Door:**
```
[Client / Other Pod]
         │
         │ calls "web-service:80"
         ▼
┌──────────────────────────────────────┐
│          Service: web-service        │
│  ClusterIP: 10.96.0.10               │
│  selector: app=web                   │
│                                      │
│  Endpoints:                          │
│  10.244.1.5, 10.244.2.3, 10.244.3.8  │
└──────────────────┬───────────────────┘
                   │ load balances
         ┌─────────┼─────────┐
         ▼         ▼         ▼
     [Pod 1]   [Pod 2]   [Pod 3]
    app=web    app=web    app=web
```

**NodePort vs ClusterIP vs LoadBalancer:**
```
Internet ──► [Cloud LB] ──► NodePort ──► ClusterIP ──► Pods
              LoadBalancer     ↑
                               └── also accessible directly
```

> **Excalidraw idea:** A reception desk (Service) in a building lobby. The desk has one phone number on the sign outside (ClusterIP). The receptionist (kube-proxy) routes incoming calls to available staff (pods) in the offices behind. Some staff leave (pod crash), the desk gets updated and routes only to present staff. The external LB is a security guard at the building entrance routing people to the reception desk.

---

## Key Terminologies

| Term | Technical Definition | Simple Explanation |
|------|---------------------|-------------------|
| **Service** | A stable network abstraction over a set of pods | The permanent address for reaching your pods |
| **ClusterIP** | A virtual IP accessible only within the cluster | Internal extension number |
| **NodePort** | Exposes the service on each node's IP at a static port | An external line via each server's IP |
| **LoadBalancer** | Provisions a cloud LB to route external traffic | A public-facing phone switchboard |
| **Endpoints** | The actual list of pod IPs backing a Service | The directory of which employees are currently in |
| **kube-proxy** | Implements Service routing rules on each node | The routing system that directs calls |
| **ClusterDNS** | Automatic DNS resolution for services (e.g., `my-svc.namespace`) | The internal phone book |
| **Headless Service** | Service with no ClusterIP — returns pod IPs directly | Skip the receptionist, get employee direct lines |

---

## Service DNS

Kubernetes automatically creates DNS entries for every Service:

```
my-service                          → same namespace
my-service.my-namespace             → cross-namespace
my-service.my-namespace.svc.cluster.local  → fully qualified
```

Pods can always reach services by name — no hardcoded IPs needed.

---

## Common Misconceptions

- **"Services run code"** — Services are a networking abstraction. They just route traffic. The pods do the actual work.
- **"I need a LoadBalancer Service for internal apps"** — ClusterIP is sufficient and more efficient for internal service-to-service communication.
- **"Services automatically balance load evenly"** — By default, kube-proxy uses random or round-robin selection. Equal distribution isn't guaranteed for long-lived connections.
- **"Deleting a Service deletes its pods"** — Services and pods are independent. Deleting a Service just removes the routing abstraction — pods keep running.

---

## Related Concepts

- [Pods](../pods/README.md) — What Services route traffic to
- [Labels & Selectors](../labels-selectors/README.md) — How Services identify their pods
- [Networking](../../03-networking/README.md) — Ingress, DNS, NetworkPolicy
- [Deployments](../deployments/README.md) — Commonly paired with Services

---

## Additional Learning Resources

- [Services — Official Docs](https://kubernetes.io/docs/concepts/services-networking/service/)
- [Service Types Explained](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)
- [DNS for Services and Pods](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)
