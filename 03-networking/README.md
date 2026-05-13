# Networking

> Status: Outline ready — detailed concept files coming soon.

## What You'll Learn

How pods, services, and the outside world communicate in Kubernetes.

---

## Topics in This Section

### 1. Kubernetes Networking Model
- Every pod gets a unique IP
- Pods can talk to any other pod without NAT
- Agents (kubelet, kube-proxy) can reach all pods

### 2. Pod-to-Pod Communication
- Same node: direct via Linux bridge
- Different nodes: routed via CNI plugin
- CNI plugins: Calico, Flannel, Cilium, Weave

### 3. Service Networking
- ClusterIP (internal)
- NodePort (node-level external)
- LoadBalancer (cloud LB)
- Headless Services

### 4. DNS in Kubernetes
- CoreDNS — the cluster DNS server
- Service DNS: `my-svc.my-namespace.svc.cluster.local`
- Pod DNS resolution

### 5. Ingress
- Routes HTTP/HTTPS traffic from outside the cluster to services
- Ingress Controllers: NGINX, Traefik, AWS ALB
- Host-based and path-based routing

### 6. NetworkPolicy
- Firewall rules for pods
- Default: all traffic allowed
- Policies restrict ingress/egress between pods

---

## Key Analogy

The cluster network is like a **private city road network**:
- Every building (pod) has its own street address (pod IP)
- There are public highways (Services) that route visitors to buildings
- The city has a gated community entrance (Ingress) for outside visitors
- Traffic rules (NetworkPolicy) control which streets are accessible

---

## Coming Soon

- `pod-to-pod.md` — How pods communicate across nodes
- `dns.md` — CoreDNS and service discovery
- `ingress.md` — Routing external HTTP traffic
- `network-policy.md` — Securing pod communication

---

## References

- [Kubernetes Networking — Official Docs](https://kubernetes.io/docs/concepts/cluster-administration/networking/)
- [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)
- [NetworkPolicy](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
