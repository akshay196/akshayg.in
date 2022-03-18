---
title: Go Variadic Function
date: 2021-05-16
tags: [go, note]
---

Example of Go variadic function:

```go
func main() {
    nums := []int{1, 2, 3}

    // uses the existing slice
    s1 := sum(nums...)

    // creates a new slice
    s2 := sum(1, 2, 3)

    // Both s1 and s2 values are equal

    // Variadic func can be called with no argument
    s3 := sum()
}

func sum(nums ...int) (total int) {
    for _, n := range nums {
        total += n
    }
}
```

The common example is the `Println` function from the `fmt` package.

```go
func Println(a ...interface{}) (n int, err error)
```
