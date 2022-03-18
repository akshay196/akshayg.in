---
title: Keyed array elements in Go
date: 2021-02-22
tags: [go, note]
---

Unkeyed array elements:

```go

example := [3]float64{
        1.3,
        6.7,
        4.0,
}

```

Keyed array elements:

```go

example := [3]float64{
        0: 1.3,
        1: 6.7,
        2: 4.0,
}

```

Keyed array in different order:

```go

example := [3]float64{
        1: 1.3,
        0: 6.7,
        2: 4.0,
}

```

Auto-initialize keyed array elements:

```go

example := [...]float64{
        // index 0 is empty
        // index 1 is empty
        2: 4.0,    // index 2
}

```

Unkeyed and keyed array elements:

```go

example := [...]float64{
        // index 1 to 4 are empty
        5: 1.3,    // index 5
        6.7,       // index 6
        0: 4.0,    // index 0
}

```
