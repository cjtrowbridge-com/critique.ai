---
layout: default
title: Gravity UI
---

# Critique.ai - Gravity UI Specification

## ✨ Project Vision: "The Enemy’s Gate Is Down"

Inspired by Ender Wiggin's realization that changed the rules of combat, ** Gravity UI** reimagines how users interact with complex data workflows. Rather than the traditional horizontal or form-based pipeline builder, **this system visualizes data as something that flows downward—falling from raw input to structured insight**.

This metaphor makes data flow natural, interpretable, and scalable. It also enables composable, modular workflows with real-time dependency propagation—unlocking arbitrarily complex chains of transformation, model application, and publishing in an intuitive visual interface.

---

## 🧠 Philosophical Foundation

### Why "Gravity"?

- Humans understand **top-down cause and effect** instinctively.
- Gravity evokes **natural flow**, **cascading logic**, and **inherent order**.
- Makes **"upstream" and "downstream" literally visible**, avoiding hidden logic.
- Aligns with how people mentally model **water systems**, **signal chains**, and **narratives** (beginning → conclusion).

---

## 🔧 Technical Overview

### Core Concepts

- **Everything is a Node**: Sources, transforms, models, outputs.
- **Data Flows Downward**: Nodes execute top → bottom.
- **Each Node Is Reactive**: When input changes, downstream nodes are invalidated.
- **No Global "Run"**: Execution happens through propagation from updated sources.

---

## 📐 Layout & UI Design

### Primary Zones

```
+-----------------------------------------------------------+
| 🛠️  Top Toolbar                                           |
|  [New] [Save] [Load] [Export JSON] [Add Node ▼]           |
+-----------------------------------------------------------+
|                                                           |
|  ⬇️   Scrollable Gravity Canvas                           |
|                                                           |
|      🌐 Source: MySQL Table                               |
|              ↓                                            |
|      💬 Node: Sentiment Classifier (LLM)                  |
|              ↓                                            |
|      🔧 Node: Join with Survey CSV                        |
|              ↓                                            |
|      🧠 Node: ANOVA                                       |
|              ↓                                            |
|      ✅ Assertion: p < 0.05                               |
|              ↓                                            |
|      📤 Publish: Dashboard JSON Export                    |
|                                                           |
+-----------------------------------------------------------+
| 📊 Status Bar (staleness, warnings, system alerts)        |
+-----------------------------------------------------------+
```

---

## 🧩 Node Structure

Each node is a modular unit that:

- Has **input(s)** and **output(s)**
- Defines a **run()** method
- Tracks **staleness**
- Emits a preview (if applicable)
- Supports configuration via the **right-hand inspector panel**

### Node Anatomy

- **Top Bar**: Title (editable), node type icon
- **Left Handles**: Input ports
- **Right Handles**: Output ports
- **Main Panel**: Optional preview table, log, or chart
- **Status Strip**: Indicator for idle 🟢, running 🔄, error ❌, stale 🟡

### Node Types

| Type         | Icon | Description |
|--------------|------|-------------|
| 🌐 Source     |      | CSV, SQL, IPFS, JSON URL, etc. |
| 🔧 Transform  |      | Join, filter, normalize, encode, derive |
| 💬 Classifier |      | LLM-driven node (e.g., sentiment analysis) |
| 🧠 Model      |      | Regression, clustering, PCA, etc. |
| ✅ Assert     |      | Tests (e.g., “no nulls”, “R² > 0.7”) |
| 📤 Output     |      | CSV, JSON, IPFS, webhook, dashboard hook |

---

## ⚙️ Data Flow and Execution Engine

### Dependency Graph

- Each node stores:
  - `List<Node> inputs`
  - `List<Node> outputs`
- When a source node is modified:
  - Its downstream nodes are marked `stale`
  - Only stale nodes are re-executed
  - All execution is **topologically sorted**

### Node Execution Lifecycle

1. Check input freshness
2. If stale, rerun `run()`
3. Update outputs and preview
4. Notify downstream nodes

---

## 📈 Canvas Interaction Model

### Navigation

- **Pan**: Click + drag background
- **Zoom**: Ctrl + mouse wheel
- **Mini-map**: Optional overview panel

### Node Operations

- **Add Node**: Drag from toolbar or context menu
- **Connect Nodes**: Click-drag from output → input
- **Move Nodes**: Drag within canvas
- **Delete Node**: Select → Delete key
- **Group Nodes**: Select + Right-click → Group

---

## 🎛️ Inspector Panel (Right Sidebar)

Visible when a node is selected.

### Tabs

1. **Config**
   - Input selectors (if needed)
   - Parameters (e.g., model depth, join keys, thresholds)
   - Assertions
2. **Preview**
   - Live output table or summary metrics
3. **Publish**
   - Select which outputs to publish
   - Auto-publish toggle
   - IPFS/Webhook targets

---

## ✅ Features

### Core Functionalities

- Real-time **graph-based dataflow execution**
- Composable pipelines using **drag-and-drop logic**
- Inline preview and **staleness tracking**
- Custom **assertion nodes**
- **Reactive propagation**: data changes → auto reruns downstream nodes
- Export pipeline to:
  - JSON spec
  - JAR job bundle
  - Dashboard-ready artifacts

---

## 💡 User Experience Goals

| Feature | Why It Matters |
|---------|----------------|
| **Vertical orientation** | Reinforces intuitive sense of data flow |
| **Node previews** | Helps users debug and validate logic in-place |
| **Assertion nodes** | Prevents bad data from publishing |
| **Config sidebars** | Reduces clutter on canvas |
| **Live reactivity** | Keeps results in sync with upstream data |
| **Grouping** | Manages complexity in large graphs |

---

## 🎯 Target Users

- **Data Scientists**: Visualize modeling pipelines without writing boilerplate
- **Analysts**: Combine public datasets and extract insights
- **Civic Technologists**: Build live, automated public dashboards
- **Educators**: Teach statistical workflows and AI transparently
- **Developers**: Prototype dataflows, then export for production integration

---

## 🧱 Development Considerations

### MVP Feature Set

- Node graph canvas (JavaFX/Swing hybrid)
- Node base class & registry
- Execution scheduler (topological sorting + caching)
- TableModel-based intermediate outputs
- IPFS-compatible publisher
- JSON dashboard exporter
- 10 node types:
  - 2 sources (CSV, SQL)
  - 2 transforms (Join, Normalize)
  - 2 models (Linear regression, PCA)
  - 1 LLM (Sentiment)
  - 1 assertion
  - 2 outputs (CSV, JSON)

---

## 📢 Marketing Language

> “What if data flowed like water, and insight fell into place?”  
>  
> Welcome to **Critique.ai**—the gravity-powered, drag-and-drop intelligence canvas. Inspired by *Ender's Game*, *ComfyUI*, and the open-ended power of *Factorio*, Critique.ai lets you visualize, build, and publish machine learning pipelines with zero clutter and maximum control.

---

## 📦 File Format & Export

- Entire graph saved/exported as a **JSON workflow spec**
- Each node serialized with:
  - `id`, `type`, `config`, `position`, `input_ids`
- Allows team collaboration, versioning, pipeline reuse

---

## 🗺️ Future Extensions

- **3D Graph Layers** (think: rows = time, columns = pipelines)
- **Collaborative Editing** (WebSocket + file locks)
- **Plugin SDK** (custom node types)
- **Code Exporter** (export graph as runnable Java/Kotlin/Python code)
- **Graph Search** (Find all nodes using column `income_level`)
- **Time Travel Debugger** (Replay state as data flowed through)

---

## 🔚 Summary

This document describes the full rationale and implementation plan for a gravity-based, vertical ML pipeline UI inspired by ComfyUI and Ender’s Game. It covers interaction design, execution models, node structures, visual metaphors, and marketing tone. The enemy’s gate is down—data doesn’t have to be trapped in flat spreadsheets or black-box clouds. Let it fall, flow, and flourish.

