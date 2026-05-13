# Analogies Index

A master reference of all real-world analogies used across this repository.

This file helps maintain consistency — the same concept always uses the same analogy world.

---

## Analogy Worlds

### The City / City Hall

The primary analogy for the overall Kubernetes cluster.

| K8s Concept | City Equivalent | File |
|-------------|----------------|------|
| Kubernetes Cluster | The city | [kubernetes-architecture.md](../../01-kubernetes-introduction/kubernetes-architecture.md) |
| Control Plane | City Hall | [control-plane.md](../../01-kubernetes-introduction/control-plane.md) |
| API Server | Mayor's desk / front door | [control-plane.md](../../01-kubernetes-introduction/control-plane.md) |
| etcd | City archives / records vault | [control-plane.md](../../01-kubernetes-introduction/control-plane.md) |
| Scheduler | Urban planner | [control-plane.md](../../01-kubernetes-introduction/control-plane.md) |
| Controller Manager | Department heads | [control-plane.md](../../01-kubernetes-introduction/control-plane.md) |
| Worker Nodes | City districts | [kubernetes-architecture.md](../../01-kubernetes-introduction/kubernetes-architecture.md) |
| Pods | Apartments in a district | [pods/README.md](../../02-core-objects/pods/README.md) |
| Namespaces | Floors in an office building | [namespaces/README.md](../../02-core-objects/namespaces/README.md) |

---

### Restaurant / Kitchen

| K8s Concept | Restaurant Equivalent | File |
|-------------|----------------------|------|
| Server | Restaurant kitchen | [what-is-a-server.md](../../00-prerequisites/what-is-a-server.md) |
| Network | Waiter | [what-is-a-server.md](../../00-prerequisites/what-is-a-server.md) |
| Client | Customer | [what-is-a-server.md](../../00-prerequisites/what-is-a-server.md) |

---

### Hotel vs Hostel

| K8s Concept | Equivalent | File |
|-------------|-----------|------|
| Virtual Machine | Hotel room (private, full-featured) | [virtualization-vs-containers.md](../../00-prerequisites/virtualization-vs-containers.md) |
| Container | Hostel bunk (shared infrastructure) | [virtualization-vs-containers.md](../../00-prerequisites/virtualization-vs-containers.md) |
| Hypervisor | Hotel manager | [virtualization-vs-containers.md](../../00-prerequisites/virtualization-vs-containers.md) |

---

### Shipping Containers / Port

| K8s Concept | Equivalent | File |
|-------------|-----------|------|
| Docker Image | Shipping container (standardized box) | [what-is-docker.md](../../00-prerequisites/what-is-docker.md) |
| Dockerfile | Blueprint for the container | [what-is-docker.md](../../00-prerequisites/what-is-docker.md) |
| Docker Hub | Port / warehouse | [what-is-docker.md](../../00-prerequisites/what-is-docker.md) |
| Server with Docker | Cargo ship | [what-is-docker.md](../../00-prerequisites/what-is-docker.md) |

---

### Postal System / Phone Book

| K8s Concept | Equivalent | File |
|-------------|-----------|------|
| IP Address | Street address | [networking-basics.md](../../00-prerequisites/networking-basics.md) |
| Port | Apartment number | [networking-basics.md](../../00-prerequisites/networking-basics.md) |
| DNS | Phone book | [networking-basics.md](../../00-prerequisites/networking-basics.md) |
| Network Packet | Sealed envelope | [networking-basics.md](../../00-prerequisites/networking-basics.md) |
| Router | Postal sorting facility | [networking-basics.md](../../00-prerequisites/networking-basics.md) |

---

### Airline Operations Center

| K8s Concept | Equivalent | File |
|-------------|-----------|------|
| Kubernetes | Airline operations center | [what-is-kubernetes.md](../../01-kubernetes-introduction/what-is-kubernetes.md) |
| Containers | Flights | [what-is-kubernetes.md](../../01-kubernetes-introduction/what-is-kubernetes.md) |
| Nodes | Airports | [what-is-kubernetes.md](../../01-kubernetes-introduction/what-is-kubernetes.md) |
| Control Plane | Flight controllers | [what-is-kubernetes.md](../../01-kubernetes-introduction/what-is-kubernetes.md) |

---

### Factory Floor

| K8s Concept | Equivalent | File |
|-------------|-----------|------|
| Worker Node | Factory floor | [worker-node.md](../../01-kubernetes-introduction/worker-node.md) |
| kubelet | Floor supervisor | [worker-node.md](../../01-kubernetes-introduction/worker-node.md) |
| kube-proxy | Internal mailroom | [worker-node.md](../../01-kubernetes-introduction/worker-node.md) |
| Container Runtime | Manufacturing machines | [worker-node.md](../../01-kubernetes-introduction/worker-node.md) |

---

### Apartment Building

| K8s Concept | Equivalent | File |
|-------------|-----------|------|
| Pod | Shared apartment | [pods/README.md](../../02-core-objects/pods/README.md) |
| Containers | Roommates | [pods/README.md](../../02-core-objects/pods/README.md) |
| Pod IP | Apartment address | [pods/README.md](../../02-core-objects/pods/README.md) |
| Shared volumes | Shared kitchen/utilities | [pods/README.md](../../02-core-objects/pods/README.md) |

---

### Franchise / Restaurant Chain

| K8s Concept | Equivalent | File |
|-------------|-----------|------|
| ReplicaSet | Franchise manager (keeps N locations open) | [replicasets/README.md](../../02-core-objects/replicasets/README.md) |
| Pod replica | Individual franchise location | [replicasets/README.md](../../02-core-objects/replicasets/README.md) |
| Deployment | Operations director (manages updates) | [deployments/README.md](../../02-core-objects/deployments/README.md) |
| Rolling update | Updating one location at a time | [deployments/README.md](../../02-core-objects/deployments/README.md) |

---

### Company Phone Number / Reception Desk

| K8s Concept | Equivalent | File |
|-------------|-----------|------|
| Service | Company's main phone number / reception | [services/README.md](../../02-core-objects/services/README.md) |
| Pod | Individual employee | [services/README.md](../../02-core-objects/services/README.md) |
| Load balancing | Routing calls to available employees | [services/README.md](../../02-core-objects/services/README.md) |

---

### Music Playlist / Color-Coded Wristbands

| K8s Concept | Equivalent | File |
|-------------|-----------|------|
| Labels | Tags on songs / patient wristbands | [labels-selectors/README.md](../../02-core-objects/labels-selectors/README.md) |
| Selectors | Playlist filters / nurse queries | [labels-selectors/README.md](../../02-core-objects/labels-selectors/README.md) |

---

## Visual Asset Ideas

Future illustrations to create for this folder:

| Filename | Description |
|----------|-------------|
| `city-cluster.png` | Full city = cluster aerial view |
| `hotel-vs-hostel.png` | VM vs Container side-by-side comparison |
| `shipping-container-docker.png` | Docker as shipping container system |
| `reception-service.png` | Service as reception desk routing calls |
| `playlist-labels.png` | Labels as song tags, selectors as filters |
| `franchise-replicaset.png` | Franchise manager with N locations |
| `rolling-update-restaurant.png` | Updating restaurants one at a time |
