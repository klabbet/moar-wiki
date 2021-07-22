## Messages

| Table of Contents                           |
| ------------------------------------------- |
| [1.1.1 Envelope](111_envelope.html)         |
| [1.1.2 Content Body](112_content_body.html) |

The only means of communication in MOAR is by messages. It doesn't matter if you're running a query, sending a command or subscribing to an event. All data communication is done through messages.

A message is a strongly typed document with two parts.

- Envelope for metadata
- Content for data body

Example of a message could look like this.

```json
{
  "id": "fad76b54-95e0-4200-a92c-baa64a3afdb8",
  "name": "get-user-profile-query",
  "type": "urn:klabbet:get-user-profile-query:1.0.0",
  "version": "1.0.0",
  "body": {
    "username": "miguel"
  }
}
```

This message is a query message for users with username "miguel".

This is the OpenAPI definition of the message.

```yaml
type: object
required:
  - id
  - name
  - type
  - version
  - body
additionalProperties: true
properties:
  id:
    type: string
    format: uuid
    example: fad76b54-95e0-4200-a92c-baa64a3afdb8
  name:
    type: string
    example: get-user-profile-query
  type:
    type: string
    format: urn
    example: "urn:klabbet:get-user-profile-query:1.0.0"
  version:
    type: string
    format: semver
    example: 1.0.0
  body:
    type: object
    example: '{ "username": "miguel" }'
```

This is the base definition of the Message component, but remember that you can extend it with your own properties as needed.

[Next &raquo;](111_envelope.html)
