---
title: iota constant in Go
date: 2021-01-26
tags: [go, note]
---

Linearly increasing or decreasing constant values can be declared
using "iota".

For example:

```go
func main() {
    const (
        monday    = 0
        tuesday   = 1
        wednesday = 2
        thursday  = 3
        friday    = 4
        saturday  = 5
        sunday    = 6
    )
}
```

This can be simplified as:

```go
func main() {
    const (
        monday    = iota // = 0
        tuesday          // = 1
        wednesday        // = 2
        thursday         // = 3
        friday           // = 4
        saturday         // = 5
        sunday           // = 6
    )
}
```

iota can be used in expression.

```go
func main() {
    const (
        Summer   = (iota + 1) * 3  // = 3
        Monsoon                    // = 6
        Winter                     // = 9
    )
}
```
