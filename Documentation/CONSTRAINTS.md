Constraints
===========

## Basics

#### Operators `+` `-` `*` `/`
E.g.
```
left == (width / 100) + 10
```

#### Comparison `==` `<=` `>=`

Useful to use the `<=` and `>=` when you want something to be
- as tall as needed
- but constrained to not being taller than 200
- and constrained to being taller than 0

Example
```
title.height >= 0
title.height == title.intrinsicHeight !strong
title.height <= title.intrinsicHeight !strong
title.height <= 200
```


### Coordinates

Unlike UIKit the coordinate system in ALE is absolute. Therefore you should always place elements relative to each other and not relative to `[0, 0]`.


WRONG
```
[
  title.left == 10
  title.right == width - 10
]
```

CORRECT
```
[
  title.left == left + 10
  title.right == right - 10
]
```
