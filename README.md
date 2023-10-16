# Moon Server Specification
Open API specification for simple file-based data (markdown, text, ...) publishing server

## What is a Moon Server?
A Moon Server is the most simplified language/technology-agnostic definition of a publishing server. Its aim is to define the absolute minimum of actions necessary for:

- Publishing notes (e.g. from Obsidian)
- Unpublishing notes
- Getting note detail by ID (generated on the server during publishment)

## Ecosystem
Any implementation following Open API specification will play nicely with [Moon Server Publisher](https://github.com/Dzoukr/MoonServerObsidianPlugin) plugin for [Obsidian](https://obsidian.md) editor.

## Minimal definition

### `GET` /detail/{id}

**Response**
```json
{
    "name": "Article ABC",
    "path": "my/folder/Article ABC.md",
    "metadata": {"id": 123, "category": "lifestyle"},
    "content": "Markdown",
    "attachments": {"image.jpg": "base64"}
}
```


### `POST` /publish/{id?}
Creates or updates item

**Body**
```json
{
    "name": "Article ABC",
    "path": "my/folder/Article ABC.md",
    "metadata": {"id": 123, "category": "lifestyle"},
    "content": "Markdown",
    "attachments": {"image.jpg": "base64"}
}
```

**Response**

Response **must** contain an object with `ID`!

```json
{
    "id" : 123,
    "anything" : "else"
}
```

### `POST` /unpublish/{id}
Removes the item

Response **must** contain an object with `ID` set to `null` or `ID` must be completely missing (so the client system knows it was successfully unpublished)!

**Response**
```json
{
    "id" : null,
    "anything" : "else"
}
```

## Open API specification
See the source code [MoonServerSpecification.yaml](MoonServerSpecification.yaml)

## What about other actions like filtering, searching, ...?
To keep the definition at its absolute minimum, this specification does not solve additional functionalities like searching, paging, sorting, grouping, and other possible list actions. It's up to every single specific Moon Server implementation to define additional logic and extended endpoints to do so.
