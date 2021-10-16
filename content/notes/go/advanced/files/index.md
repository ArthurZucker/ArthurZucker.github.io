---
title: File Manipulation
weight: 40
menu:
  notes:
    name: File Manipulation
    identifier: notes-go-advanced-files
    parent: notes-go-advanced
    weight: 10
---

<!-- Condition -->
{{< note title="Condition">}}

```go
if day == "sunday" || day == "saturday" {
  rest()
} else if day == "monday" && isTired() {
  groan()
} else {
  work()
}
```

```go
if _, err := doThing(); err != nil {
  fmt.Println("Uh oh")
```

```html
{{<mermaid align="left">}}
graph LR;
    A[Hard edge] -->|r=0| B(a<sub>0</sub>)
    B --> C{Decision}
    C -->|One| D[Result one]
    C -->|Two| E[Result two]
{{< /mermaid >}}
```
{{< /note >}}


<!-- Condition -->
{{< note title="mermaid">}}
```html
{{<mermaid align="left">}}
graph LR;
    A[Hard edge] -->|r=0| B(a<sub>0</sub>)
    B --> C{Decision}
    C -->|One| D[Result one]
    C -->|Two| E[Result two]
{{< /mermaid >}}
```
{{< /note >}}