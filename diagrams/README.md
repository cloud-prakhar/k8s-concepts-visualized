# Diagrams

This folder contains exported diagram files for all concepts in this repository.

---

## Diagram Index

| Concept | Suggested Filename | Type | Status |
|---------|-------------------|------|--------|
| Full Cluster Architecture | `cluster-architecture.png` | Technical | Planned |
| VM vs Container | `vm-vs-container.png` | Comparison | Planned |
| Docker Build→Ship→Run | `docker-build-ship-run.png` | Flow | Planned |
| Control Plane Internals | `control-plane.png` | Technical | Planned |
| Worker Node Internals | `worker-node.png` | Technical | Planned |
| Pod Anatomy | `pod-anatomy.png` | Technical | Planned |
| ReplicaSet Self-Healing | `replicaset-healing.png` | Flow | Planned |
| Deployment Rolling Update | `deployment-rolling-update.png` | Flow | Planned |
| Service Types | `service-types.png` | Technical | Planned |
| Label Selector Filtering | `label-selector.png` | Conceptual | Planned |
| Namespace Isolation | `namespaces.png` | Technical | Planned |
| Scheduling Flow | `scheduling-flow.png` | Flow | Planned |

---

## Diagram Style Guide

**Colors (consistent palette):**
- Kubernetes objects: `#3970e4` (K8s blue)
- Containers/Apps: `#2ecc71` (green)
- Networking: `#e67e22` (orange)
- Storage: `#9b59b6` (purple)
- Control Plane: `#e74c3c` (red)
- External/Cloud: `#95a5a6` (grey)

**Shapes:**
- Rounded rectangles → components and pods
- Cylinders → storage
- Cloud shape → external services
- Dashed border → logical groupings (namespaces, clusters)

**Arrows:**
- Solid arrow `→` → direct communication
- Dashed arrow `-->` → indirect/eventual
- Label all arrows with what flows through them

**Layout principles:**
- One idea per diagram — no clutter
- Title at top
- Legend if more than 3 colors used
- Keep it readable at 800px width

---

## Recommended Tools

| Tool | Best For | Link |
|------|---------|------|
| Excalidraw | Quick, hand-drawn style | [excalidraw.com](https://excalidraw.com) |
| draw.io | Detailed technical diagrams | [draw.io](https://draw.io) |
| Mermaid | Diagrams-as-code in Markdown | [mermaid.js.org](https://mermaid.js.org) |
| Lucidchart | Collaboration at team scale | [lucidchart.com](https://www.lucidchart.com) |

---

## Contributing Diagrams

1. Create the diagram in Excalidraw (save the `.excalidraw` source file too)
2. Export as PNG at 2x resolution
3. Name it following the index above
4. Drop it in this `/diagrams` folder
5. Update the index table with status: **Done**
