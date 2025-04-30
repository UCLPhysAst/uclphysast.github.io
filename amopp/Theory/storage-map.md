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
``` mermaid
graph LR
  A[Node] --> B[Scratch];
  B -->|Temp| C[Scratch];
  B -->|Temp -> | C[Void];
  B -->|6-12 Months| C[Silo];
  B -->|Permanent| C[Project Moon];
  B[Start] --> D{Error?};
```