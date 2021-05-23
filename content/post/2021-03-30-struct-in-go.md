---
title: Struct in Go
date: 2021-03-30
tags: [go, note]
---

Declare a struct:

```go
type person struct {
    name, lastname   string
    age              int
}

var alice struct {
    name, lastname   string
    age              int
}
```

Struct instance:

```go
picasso := person{
    name:     "Pablo",
    lastname: "Picasso",
    age:      91,
}

alice.name = "Alice"
alice.lastname = "Wonderland"
alice.age = 21
```

**Note**: Struct can be compared. You can't compare struct values that
contains incomparable fields. You need to compare them manually.

Embed struct to another struct:

```go
type text struct {
    title string
    words int
}

type book struct {
    // embed the text
    text
    isbn  string
}
```

Say b1 is instance of book stuct, then `b1.title` is equal to
`b1.text.title` and `b1.words` is equal to `b1.text.words`.
