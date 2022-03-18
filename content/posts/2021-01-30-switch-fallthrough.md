---
title: Go Switch fallthrough
date: 2021-01-30
tags: [go, note]
---

Switch cases in go can use ``fallthrough`` keyword to fall into next
case without checking it's condition if the current case has
fallthrough statement at the end.

For example:

```go
    i := 142

	switch {
	case i > 100:
		fmt.Print("big ")
		fallthrough
	case i > 0:
		fmt.Print("positive ")
		fallthrough
	default:
		fmt.Print("number")
	}

```

The output is,

```
big positive number
```

"fallthrough" can be used in scenario where the block of both cases
are same. It avoids duplication of code.
