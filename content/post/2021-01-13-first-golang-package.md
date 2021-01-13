---
title: My first golang package
date: 2021-01-13
tags: [go]
---

Here is my first golang package,
https://github.com/akshay196/golang. It is pretty simple package that
only contains a function `Version()`.  The function returns go version
string.

How to use?

Run command:

```
$ go get github.com/akshay196/golang
```

Then use package in your go code:

```
package main

import (
    "fmt"
    "github.com/akshay196/golang"
)

func main() {
    fmt.Println(golang.Version())
}
```

This is done as part of exercise in
[learngo](https://github.com/inancgumus/learngo).
