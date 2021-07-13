## Messages

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

### Envelope

The message envelope is a key/value store with a predetermined set of properties.

| Property | Type     | Description                        | Example                                    |
| -------- | -------- | ---------------------------------- | ------------------------------------------ |
| id       | GUID     | Unique message identifier.         | `fad76b54-95e0-4200-a92c-baa64a3afdb8`     |
| name     | String   | Name of the message.               | `get-user-profile-query`                   |
| schema   | URN      | Type descriminator of the message. | `urn:klabbet:get-user-profile-query:1.0.0` |
| version  | Version  | Version of the message schema.     | `1.0.0`                                    |
| body     | Document | The body of the message.           | `{ "username": "miguel" }`                 |

These properties are required in an envelope, and they are required to come in exactly this order.

#### ID Property

The ID is generated upon creation of the message and it is the source service that is sending the message that is also generating the id. This property must be unique for all messages in order for the system to distinguish if it has recieved the same message twice, or if it's recieving a new message with the same body.

The ID property should always be a GUID.

#### Name Property

The Name property tells the reciever how it should handle the message. The reciever will map the name of the message with a handler.

The name property should have the following format

> `{action}-{object}-{operation}`

In the example above `get` is the action, `user-profile` is the object and `query` is the operation. Please see [Operations section](300_operations.html) for possible operations.

#### Schema Property

This is a type descriminator of the body content, but we avoid calling it "type" as that is a reserved keyword in many programming languages.

It defines the type or schema of the contents of body. It should have the following format.

> `urn:{namespace}:{type name}:{version}`

The namespace part is important if you run several different systems that interconnect and the definition of a "user profile" is not the same. Then you use the namespace to separate what kind of "user profile" this message contains.

Type name is not the same as the name property, but it could be. You could easily reuse a type in several different messages that have different actions or operations.

Version is the version of the schema. It should always be updated if the schema is updated. [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html) applies here.

#### Version Property

The reciever will use the version property to decide if it could handle the message or not. For this it will use the [NPM semantic versioning scheme](https://docs.npmjs.com/about-semantic-versioning).

This value will most often be the same as the schema version, but if the sender has added metadata to the envelope that the reciever must be able to parse, the version property can indicate it by incrementing the major version.

This version is always [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

#### Extending the Envelope

You can extend the envelope with your own properties. These extensions should always come before `body` but after `version`.

Example of data you might want to add is, authorization tokens, expected content types.

## Message Body

Oh boy.

### Transport Independence

The MOAR architecture does not interfere whith the data transport of your messages. You could send messages in XML, JSON, BSON or a properitary format of your own. What's important is that the same message that was sent is also recieved without modifications.

For instance, the transportation layer may not attach extra ID, timestamps or debug information to the message.
