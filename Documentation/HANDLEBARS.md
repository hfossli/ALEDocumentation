Handlebars
==========

Document
```javascript
{
  "user": {
    "first_name": "Ottar",
    "last_name": "Salvesen"
  }
}
```

Template example 1

```javascript
{
  "id": "title",
  "type": "text",
  "text": "Hello {{user.first_name}} {{user.last_name}}!"
}
```

Template example 2

```javascript
{
  "id": "user_info",
  "type": "user_info",
  "user": "{{user}}"
}
```
