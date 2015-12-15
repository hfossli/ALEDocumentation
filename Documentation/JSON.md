
JSON Basics
===========

This is a node spec

```javascript
{
  "constraints": [
    "title.left == left + 10",
    "title.right == right - 10",
    "title.top == top + 10"
    "title.height == title.intrinsicHeight"
  ],
  "children": [
    {
      "id": "title",
      "type": "text",
      "text": "Hello {{user.first_name}}!"
    }
  ]
}
```

You can have a tree of nodespecs

```javascript
{
  "constraints": [],
  "children": [
    {
      "id": "...",
      "constraints": [],
      "children": [
        {
          "id": "...",
          "constraints": [],
          "children": []
        }
      ]
    },
    {
      "id": "...",
    }
  ]
}
```

## [Handlebars](/Documentation/HANDLEBARS.md)

```javascript
{
  "id": "text",
  "text": "Hello {{user.first_name}}"
}
```

See more examples [here](/Documentation/HANDLEBARS.md).

## Best practices

#### Don't use id for top level objects

WRONG
```javascript
{
  "id": "main",  < - - - - - -
  "type": "foo",
  "constraints": [],
  "children": [
    {
      "id": "title",
      ...
    }
  ]
}
```

CORRECT
```javascript
{
  "type": "foo",
  "constraints": [],
  "children": [
    {
      "id": "title",
      ...
    }
  ]
}
```

#### Coordinates are absolute

Unlike UIKit the coordinate system in ALE is absolute. Therefore you should always place elements relative to each other and not relative to `[0, 0]`.

WRONG
```javascript
[
  "title.left == 10",
  "title.right == width - 10"
]
```

CORRECT
```javascript
[
  "title.left == left + 10",
  "title.right == right - 10"
]
```
