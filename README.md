# MoonServerSpecification
Open API specification for simple file-based data (markdown, text, ...) publishing server

## What is a Moon Server?
A Moon Server is the most simplified language/technology-agnostic definition of a publishing server. Its aim is to define the absolute minimum of actions necessary for:

- Publishing notes (e.g. from Obsidian)
- Unpublishing notes
- Getting note detail by ID (generated on the server during publishment)

## Minimal definition

### `GET` /detail/{id}

**Response**
```json
{
  name : "Article ABC",
  path : "my/folder/Article ABC.md",
  metadata : [{ key : "category", value : "test" }],
  content : "Markdown",
  attachments : [{ filename : "image.jpg", payload : "base64" }]
}
```


### `POST` /publish/{id?}
Creates or updates item

**Body**
```json
{
  name : "Article ABC",
  path : "my/folder/Article ABC.md",
  metadata : [{ key : "category", value : "test" }],
  content : "Markdown",
  attachments : [{ filename : "image.jpg", payload : "base64" }]
}
```

**Response**
```json
{
  id : "123"
}
```

### `POST` /unpublish/{id}
Removes the item

**Response**
```text
empty
```

## Open API specification
See the source code [MoonServerSpecification.yaml](MoonServerSpecification.yaml)
