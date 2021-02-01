---
title: break and continue labels
date: 2021-02-01
tags: [go, note]
---

`break` and `continue` statements can be use with label in Go, similar
to `goto` statement. It is optional. Scope of labels are limited to
the function and does not conflict with variable name, as it live in
separate space. break and continue with label is only used in for,
switch and select statements.

```go
OuterLoop:
    for i := 0; i < 3; i++ {
        for j := 0; j < 3; j++ {
            fmt.Printf("i=%v, j=%v\n", i, j)
            break OuterLoop
        }
    }

```

Output:
```
i=0, j=0
```

Above example _breaks_ outer loop.

```go
OuterLoop:
    for i := 0; i < 3; i++ {
        for j := 0; j < 3; j++ {
            fmt.Printf("i=%v, j=%v\n", i, j)
            continue OuterLoop
        }
    }

```

Output:
```
i=0, j=0
i=1, j=0
i=2, j=0
```

continue with label continues the iteration of variables.

