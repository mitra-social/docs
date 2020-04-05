# Backend notes

## Activity Pub type conversion
### Link type
A link type can be represented as a string without loosing information, if only the `href` attribute is set.

```
{
  "type": "Link",
  "href": "https://example.com"
}
```

is the same as:

```
"https://example.com"
```

on the other side a string can be converted to a `Link` type in any case with only the `href` attributed set.
