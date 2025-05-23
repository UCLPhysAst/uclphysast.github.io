---
title: Storage Map
categories:
 -
---
``` mermaid
graph LR
  A[Node] -->|3 Months| B[Scratch];
  B -->|Temp| C[Scratch];
  B -->|Temp -> | C[Void];
  B -->|6-12 Months| C[Void];
  B -->|Permanent| D[Silos];
  B -->|Permanent| E[Project Moon];
  B[Scratch] --> F{Delete/Bin?};
```