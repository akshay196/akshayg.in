---
title: Run multiple go files in a same package
date: 2021-01-06
tags: [go]
---

Suppose we have multiple go files, for example greet.go, bye.go and
main.go in same directory and all have same package name. The main.go
is calling `greet()` function from greet.go, similary greet.go is
calling `bye()` from bye.go.

In this case how to run this, so that it successfully call functions
from other go files.

Simply run `go run *.go` or `go build`. `go build` will generate
binary with name similar to the directory that contains files.

Program throws an error `Undefined <Func-name>` if only run `go run
main.go`.
