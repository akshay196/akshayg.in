---
title: Slice append function in Go
date: 2021-02-26
tags: [go, note]
---

Append an element to the slice:

```go
nums := []int{1, 2, 3}
nums = append(nums, 4)
```

Append multiple elements to the slice:

```go
nums := []int{1, 2}
nums = append(nums, 3, 4)
```

Append slice to another slice:

```go
nums := []int{1, 2}
tens := []int{11, 12}
nums = append(nums, tens...)

// nums is {1, 2, 11, 12}
```
