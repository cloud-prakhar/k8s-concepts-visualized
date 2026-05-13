# Deployments

## What is it?

A Deployment is a Kubernetes object that manages the rollout and lifecycle of ReplicaSets. It provides declarative updates for pods — you describe the desired state (image version, replica count, update strategy) and the Deployment controller makes it happen, including zero-downtime updates and rollbacks.

---

## In Simple Language

A Deployment is the object you'll use 90% of the time in Kubernetes to run your applications.

It wraps a ReplicaSet (which wraps Pods) and adds one critical thing: **managed updates**. Tell it "run version 2 of my app," and it'll carefully replace old pods with new ones without taking your service down.

Think of a Deployment as "a ReplicaSet + history + update strategy."

---

## Real World Analogy

A Deployment is like a **restaurant chain operations director**:

- Manages multiple franchise locations (ReplicaSet → Pods)
- When rolling out a new menu (new app version), doesn't close all locations at once
- Uses a **rolling update**: updates one location at a time — customers never find all locations closed
- If the new menu gets terrible reviews (update fails), rolls back all locations to the old menu
- Keeps a history of past menu versions in case you need to revert

The Franchise Manager (ReplicaSet) just keeps locations open. The Operations Director (Deployment) handles the *changes*.

---

## Why This Exists

ReplicaSets alone can't update apps safely. If you change the pod template in a ReplicaSet, it doesn't automatically update existing pods.

Deployments solve the update problem:
- **Rolling updates:** Replace pods gradually, not all at once
- **Zero downtime:** Old pods serve traffic until new ones are ready
- **Rollback:** One command to revert to any previous version
- **Update history:** Full record of what changed and when
- **Pause/resume:** Mid-update control when something looks wrong

---

## How It Works

### Creating a Deployment
1. You define desired state: image, replicas, update strategy
2. Deployment creates a **ReplicaSet** with a pod template
3. ReplicaSet creates the specified number of pods
4. Pods run on nodes

### Rolling Update (default strategy)
When you update the container image:
```
Deployment v1 (RS1: 3 pods)
         │
         │  "Update to v2"
         ▼
Creates RS2 (v2 pods), starts scaling up
         │
         │  New pod ready? → Scale down RS1 by 1
         │  Repeat until RS2=3, RS1=0
         ▼
Deployment v2 (RS2: 3 pods, RS1: 0 pods but kept for rollback)
```

### Rollback
```
kubectl rollout undo deployment/my-app
         │
         ▼
Deployment scales RS1 back up, scales RS2 down
         │
         ▼
Back to v1 pods running
```

---

## Visual Diagram

**Deployment Object Hierarchy:**
```
┌──────────────────────────────────────────────────────┐
│                     Deployment                       │
│  image: myapp:v1 → myapp:v2  replicas: 3             │
│                                                      │
│  ┌──────────────────────────────────────────────┐    │
│  │            ReplicaSet (v2) ← current         │    │
│  │  ┌───────┐  ┌───────┐  ┌───────┐             │    │
│  │  │ Pod 1 │  │ Pod 2 │  │ Pod 3 │             │    │
│  │  │  v2   │  │  v2   │  │  v2   │             │    │
│  │  └───────┘  └───────┘  └───────┘             │    │
│  └──────────────────────────────────────────────┘    │
│                                                      │
│  ┌──────────────────────────────────────────────┐    │
│  │       ReplicaSet (v1) ← kept for rollback    │    │
│  │       replicas: 0 (scaled down, not deleted) │    │
│  └──────────────────────────────────────────────┘    │
└──────────────────────────────────────────────────────┘
```

**Rolling Update Visualization:**
```
Step 1:  [v1][v1][v1]         RS1=3, RS2=0
Step 2:  [v1][v1]   [v2]      RS1=2, RS2=1
Step 3:  [v1]    [v2][v2]     RS1=1, RS2=2
Step 4:      [v2][v2][v2]     RS1=0, RS2=3 ✓
```

> **Excalidraw idea:** A timeline strip showing 4 snapshots of the update process. Each snapshot shows 3 restaurant locations — old ones in blue, new ones in green. Gradually blue becomes green one at a time. An arrow below shows "traffic continues throughout" with no breaks.

---

## Key Terminologies

| Term | Technical Definition | Simple Explanation |
|------|---------------------|-------------------|
| **Deployment** | Object managing ReplicaSet lifecycle with update support | The highest-level manager for running apps |
| **Rolling Update** | Gradually replacing old pods with new ones | Updating restaurants one at a time, never closing all |
| **Rollback** | Reverting to a previous Deployment version | Switching back to the old menu |
| **Revision** | A snapshot of a Deployment's history | A saved version you can roll back to |
| **maxSurge** | How many extra pods can exist during an update | Allowed temporary overage (e.g., 4 pods during a 3-pod update) |
| **maxUnavailable** | How many pods can be unavailable during an update | Maximum disruption allowed (e.g., 1 pod offline at a time) |
| **Recreate Strategy** | Stop all old pods, then start all new pods | Kill all locations, then reopen — causes downtime |
| **Paused Deployment** | Update suspended mid-rollout | Pressed "pause" on the rolling update |

---

## Common Misconceptions

- **"Deployments run containers"** — Deployments manage ReplicaSets, which manage Pods, which contain containers. The Deployment itself doesn't run anything.
- **"Old ReplicaSets are deleted after an update"** — Old ReplicaSets are kept (scaled to 0) for rollback. They're cleaned up only after exceeding the revision history limit.
- **"Rolling updates mean zero risk"** — If your new version has bugs, they'll affect pods as they're updated. Use readiness probes and canary deployments for safer releases.
- **"Deployments are the only way to run pods"** — StatefulSets, DaemonSets, and Jobs are other workload controllers for different use cases.

---

## Related Concepts

- [ReplicaSets](../replicasets/README.md) — What Deployments manage
- [Pods](../pods/README.md) — What ReplicaSets manage
- [Services](../services/README.md) — Routes traffic to Deployment pods
- [Scaling](../../06-scaling/README.md) — HPA scales Deployments automatically

---

## Additional Learning Resources

- [Deployments — Official Docs](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [Rolling Update Strategy](https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/)
- [Deployment Strategies Explained](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#strategy)
