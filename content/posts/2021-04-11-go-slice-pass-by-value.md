---
title: Pass slice to a function
date: 2021-04-11
tags: [go, note]
---

Here is an example of slice passed as value to a function:

```go

func main() {
    dirs := []string{"up", "down", "left", "right"}
    up(dirs)

    // dirs => []string{"UP", "DOWN", "LEFT", "RIGHT"}
}

func up(list []string) {
    // slice pointer points to a reference
    // even if they passed in a function.
    // So it modify the original slice
    // elements to upper case.
    for i := range list{
        list[i] = strings.ToUpper(list[i])
    }

    // Here append function only modifies
    // the copy of slice. So the original slice
    // if unaffected by append function.
    list = append(list, "HEISEN BUG")
}

```

Here is the [link](https://blog.golang.org/slices-intro) for slice
internals.
