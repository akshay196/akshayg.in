---
title: Input Scanning using bufio in Go
date: 2021-03-25
tags: [go, note]
---

Read standard input by line:

```go
import (
    "bufio"
    "os"
    "fmt"
)

func main() {
    // New scanner to read from stdin.
    // By default it reads line. ie. split
    // function defaults to ScanLines.

    in := bufio.NewScanner(os.Stdin)
    for in.Scan() {
        // Read line and print it.
        fmt.Println(in.Text())
    }
}
```

Read by words:

```go
// Set split function to ScanWords before Scan() function.

in.Split(bufio.ScanWords)

for in.Scan() {
    ...
}
```

Capture an error in scanning:

```go
// in.Err returns first non-EOF error that was encountered in scanner.

if err := in.Err(); err != nil {
    fmt.Println("ERROR:", err)
}
```
