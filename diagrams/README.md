# Diagrams

This folder contains exported diagram files for all concepts in this repository.

---

## Diagram Index

| Concept | Excalidraw Source | Type | Status |
|---------|-------------------|------|--------|
| Full Cluster Architecture | `cluster-architecture.excalidraw` | Technical | ✅ Done |
| VM vs Container | `vm-vs-container.excalidraw` | Comparison | ✅ Done |
| Docker Build→Ship→Run | `docker-build-ship-run.excalidraw` | Flow | ✅ Done |
| Control Plane Internals | `control-plane.excalidraw` | Technical | ✅ Done |
| Worker Node Internals | `worker-node.excalidraw` | Technical | ✅ Done |
| Pod Anatomy | `pod-anatomy.excalidraw` | Technical | ✅ Done |
| ReplicaSet Self-Healing | `replicaset-healing.excalidraw` | Flow | ✅ Done |
| Deployment Rolling Update | `deployment-rolling-update.excalidraw` | Flow | ✅ Done |
| Service Types | `service-types.excalidraw` | Technical | ✅ Done |
| Label Selector Filtering | `label-selector.excalidraw` | Conceptual | ✅ Done |
| Namespace Isolation | `namespaces.excalidraw` | Technical | ✅ Done |
| Scheduling Flow | `scheduling-flow.excalidraw` | Flow | ✅ Done |

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

1. Open the `.excalidraw` file in VSCode (requires the **Excalidraw** extension by Henning Dieterichs)
2. Edit the diagram visually in VSCode — all changes auto-save to the JSON source file
3. Export as PNG at 2x resolution (Excalidraw menu → Export → PNG)
4. Name the PNG following the filename in the index above and drop it in this folder
5. Update the index table with status: **Done**

> **Tip:** The `.excalidraw` files are the source of truth. Always commit them alongside exported PNGs so diagrams stay editable.
