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
``` mermaid
sequenceDiagram
  autonumber
  Alice->>John: Hello John, how are you?
  loop Healthcheck
      John->>John: Fight against hypochondria
  end
  Note right of John: Rational thoughts!
  John-->>Alice: Great!
  John->>Bob: How about you?
  Bob-->>John: Jolly good!
```