# Observability

> Status: Outline ready — detailed concept files coming soon.

## What You'll Learn

How to know what's happening in your Kubernetes cluster — when things work and when they don't.

---

## The Three Pillars of Observability

| Pillar | What It Tells You | K8s Tools |
|--------|------------------|-----------|
| **Logs** | What happened (events, errors) | kubectl logs, Fluentd, Loki |
| **Metrics** | How things are performing (numbers) | Prometheus, Metrics Server |
| **Traces** | How requests flow through services | Jaeger, Zipkin, OpenTelemetry |

---

## Topics in This Section

### 1. Pod Logs
- Every container writes to stdout/stderr
- `kubectl logs pod-name` — view logs
- Logs are ephemeral — need a log aggregation solution for production

### 2. Liveness Probes
- Kubernetes checks if a container is alive
- If it fails: container is restarted
- Types: HTTP GET, TCP socket, exec command

### 3. Readiness Probes
- Kubernetes checks if a container is ready to serve traffic
- If it fails: pod is removed from Service endpoints (no traffic sent)
- Unlike liveness — pod isn't restarted, just isolated

### 4. Startup Probes
- Gives slow-starting containers time to initialize before liveness checks begin
- Prevents liveness probes from killing containers during startup

### 5. Metrics Server
- Lightweight in-cluster metrics collector
- Provides `kubectl top nodes` and `kubectl top pods`
- Required for HPA to work

### 6. Prometheus + Grafana
- Prometheus: scrapes and stores metrics from pods and cluster components
- Grafana: visualizes metrics as dashboards
- The de facto observability stack for Kubernetes

---

## Key Analogy

Observability is like the **instrument panel in an airplane**:
- **Logs** = the black box recording every event
- **Metrics** = the gauges showing speed, altitude, fuel level right now
- **Probes** = the automated health checks before takeoff and during flight
- **Traces** = the flight path recording showing exactly where the plane was and when

A pilot flying blind has no idea what's happening. A cluster without observability is the same.

---

## Coming Soon

- `pod-logs.md` — Accessing and aggregating logs
- `health-probes.md` — Liveness, readiness, startup probes
- `metrics-server.md` — Basic cluster metrics
- `prometheus-grafana.md` — Production monitoring stack

---

## References

- [Logging Architecture](https://kubernetes.io/docs/concepts/cluster-administration/logging/)
- [Configure Liveness and Readiness Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)
- [Prometheus](https://prometheus.io/docs/introduction/overview/)
