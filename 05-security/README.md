# Security

> Status: Outline ready — detailed concept files coming soon.

## What You'll Learn

How Kubernetes controls who can access what, and how to protect sensitive data.

---

## The Security Layers

Kubernetes security follows a **defense in depth** approach:
1. Who can access the cluster? (Authentication)
2. What can they do? (Authorization / RBAC)
3. What can they access? (NetworkPolicy, Secrets)
4. What can pods do? (Pod Security, ServiceAccounts)

---

## Topics in This Section

### 1. RBAC (Role-Based Access Control)
- **Role** — Permissions within a namespace
- **ClusterRole** — Permissions across the whole cluster
- **RoleBinding** — Grants a Role to a user/service account
- **ClusterRoleBinding** — Grants a ClusterRole globally

### 2. ServiceAccounts
- An identity for pods to authenticate to the API Server
- Every pod gets a default ServiceAccount
- RBAC policies can be attached to ServiceAccounts

### 3. Secrets
- Store sensitive data (passwords, tokens, certificates) separately from code
- Base64 encoded at rest (not encrypted by default — use encryption-at-rest configuration)
- Injected into pods as environment variables or volume mounts

### 4. ConfigMaps
- Store non-sensitive configuration data
- Decouple configuration from container images
- Injected into pods the same way as Secrets

### 5. NetworkPolicy
- L3/L4 firewall rules for pod communication
- Default: all traffic allowed
- NetworkPolicies define ingress/egress allow-lists

### 6. Pod Security
- PodSecurityContext — controls user/group, read-only filesystem, capabilities
- SecurityContext — container-level security settings
- Pod Security Admission (PSA) — enforce security standards cluster-wide

---

## Key Analogy

RBAC is like an **office access badge system**:
- **Role** = a badge that grants access to specific rooms on one floor (namespace)
- **ClusterRole** = a master badge that works on all floors
- **RoleBinding** = assigning that badge to an employee
- **ServiceAccount** = the badge assigned to a robot/automated system

---

## Coming Soon

- `rbac.md` — Roles, ClusterRoles, Bindings
- `secrets.md` — Managing sensitive data
- `configmaps.md` — Managing configuration
- `network-policy.md` — Pod-level firewall rules
- `pod-security.md` — Container security contexts

---

## References

- [RBAC — Official Docs](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
- [Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)
- [ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
- [Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
