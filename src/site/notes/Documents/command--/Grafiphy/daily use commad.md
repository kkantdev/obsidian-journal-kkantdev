---
{"dg-publish":true,"permalink":"/documents/command/grafiphy/daily-use-commad/","dg-note-properties":{}}
---

If you're using **Graphify for vibe coding in Antigravity**, there are only a few commands you'll use regularly.

### 1. Install Graphify into Antigravity (one time only)

```
graphify antigravity install
```

This sets up Antigravity so it knows about Graphify and registers the `/graphify` command. You only do this once (or after reinstalling/upgrading).

### 2. Build the graph (most important command)

Open your project in Antigravity, then run:

```
/graphify .
```

The `.` means "scan the current project."

This creates:

```
graphify-out/├── graph.html├── GRAPH_REPORT.md└── graph.json
```

You'll run this whenever you start a new project or after making lots of changes.

### 3. Update the graph after coding

Instead of rebuilding everything:

```
/graphify . --update
```

This updates only the files that changed, which is much faster.

### 4. Ask questions about your codebase

```
/graphify query "How does authentication work?"
```

or

```
/graphify query "Where is the payment flow?"
```

This lets Graphify answer from its knowledge graph instead of rereading the entire codebase.

### 5. Find connections

```
/graphify path "LoginController" "Database"
```

This shows the relationship between two parts of your project.

### 6. Explain a component

```
/graphify explain "UserService"
```

It summarizes everything Graphify knows about that class, module, or concept.