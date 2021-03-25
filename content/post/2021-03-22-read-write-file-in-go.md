---
title: Read Write files in Go
date: 2021-03-22
tags: [go, note]
---

Package ioutil implements I/O functions.

```go
import "ioutil"
```

Read file:

```go
config, error := ioutil.ReadFile("/etc/config")
```

Write to file:

```go
error := ioutil.WriteFile("/etc/config", config, 0644)
```

Read direcrtory:

```go
// ioutil.ReadDir returns slice of os.FileInfo
files, error := ioutil.ReadDir("/home/akshay")

if error != nil {
    // Handle error
}

for _, file := range files {
    // file.Size()
    // file.Name()
    // file.IsDir()
}
```

For more functions, read [ioutil](https://pkg.go.dev/io/ioutil) doc.
