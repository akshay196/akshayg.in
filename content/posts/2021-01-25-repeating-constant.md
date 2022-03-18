---
title: Repeating constant with same value
date: 2021-01-25
tags: [go, note]
---

If multiple constants have same value.

```go
	const (
		min int = 1
		max int = 1
	)
```

Then the constant declaration can be simplified as below:

```go
	// constants repeat the previous type and expression
	const (
		min int = 1
		max     // int = 1
	)
}
```
