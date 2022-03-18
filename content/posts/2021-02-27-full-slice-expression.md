---
title: Full slice expression
date: 2021-02-27
tags: [go, note]
---

Simple slice expression:

"[low:high]"

```go
numbers := [10]int{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
s := numbers[1:4]
fmt.Println(s)           // [1, 2, 3]
fmt.Println(len(s))      // len = 3
fmt.Println(cap(s))      // cap = 9
```

Full slice expression:

"[low:high:max]"

```go
numbers := [10]int{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
s := numbers[1:4:5]
fmt.Println(s)           // [1, 2, 3]
fmt.Println(len(s))      // len = 3
fmt.Println(cap(s))      // cap = 4
```

Full slice expression can be used for limit backing array sharing.

```go
nums := []int{1, 2, 3, 4}
portion := nums[:2]
portion = append(portion, 5, 6)

// portion is {1, 2, 5, 6}
// nums is {1, 2, 5, 6}
```

Above use of simple slice expression change the backing array as well.

However full slice expression limit backing array sharing (does not
modify backing array):

```go
nums := []int{1, 2, 3, 4}
portion := nums[:2:2]
portion = append(portion, 5, 6)

// portion is {1, 2, 3, 4}
// nums is {1, 2, 5, 6}
```


