---
title: Type hinting and Mypy
date: 2018-08-18
tags: [Python, Mypy]
---

Python is dynamic typed language, but static type variable can be
possible if we use type annotations. Python 3.5 and later versions
have functionality of type hinting. Though It is completely optional.

Type hinting is useful for testing purpose in CI. It does not change
code to static variable; but it make easy to understand code that you
have written long time ago.

Simple example of type hinting:

```python
>>> number: int = 10
>>> name: str = "Akshay"
```

Let's see following funtion,
```python
# file.py

def addme(a: int, b: int) -> int:
    return a + b

addme(5, 10)
```

Above code indicate that `addme()` takes 2 integer parameters (a and
b) and returns **int** value. `->` symbol shows return value type.

## Mypy

Mypy is a static type checker. To install it from
[PyPI](https://pypi.org/) run:

```bash
$ pip3 install mypy
```

Once Mypy is installed, we can check types using following command,

```bash
$ mypy file.py
```

There is no any output if types are correct as per type annotations
given in code.

In an example of `addme()`, if we change to `addme(4, "a")` and run
mypy. It shows error as,

```bash
$ mypy file.py
file.py:4: error: Argument 2 to "addme" has incompatible type "str"; expected "int"
```

## Type hinting for List, Dict and Tuple

For this we need to import the following:

```python
from typing import Tuple, Dict, List
```

Let's look at an example of type hinting for List, Dict and Tuple,

```python
# list name foobar and all the items in the list are int type
foobar: List[int] = [2, 3]

# Similarly for Dict and Tuple
alpha: Dict[int, str] = {1: "a"}
beta: Tuple[int, str, float] = (1, "text", 3.6)
```

## Reference links

1. [www.mypy-lang.org](www.mypy-lang.org)
2. [pyre-check.org](pyre-check.org) (Another Type checher)
3. [MonkeyType](https://github.com/instagram/MonkeyType): System for Python
   that genarate static type annotations
4. [https://docs.python.org/3/library/typing.html](https://docs.python.org/3/library/typing.html)
5. The [talk](https://www.youtube.com/watch?v=pMgmKJyWKn8) about type checking
