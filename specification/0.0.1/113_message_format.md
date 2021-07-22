### Message Format

The MOAR architecture does not interfere whith the data transport of your messages. You could send messages in XML, JSON, BSON or a properitary format of your own. What's important is that the same message that was sent is also recieved without modifications.

For instance, the transportation layer may not attach extra ID, timestamps or debug information to the message.

#### Message Size

The maximum size of a message is 1 MB (1024 KB). This is the maximum size of the complete serialized data in your selected message format. A message that exceed this limitation is rejected.

The reason to keep message sizes to a minimum is that they clog the system. A large message will represent a higher latency, take a longer time to process, and that will have other services wait for that message.

Querying a dataset might return a larger result than 1 MB. In that case you should look into pagination of that data.

If one data record exceeds 1 MB in size, you should look into deeplinking that data. For instance, you could upload the data to a blob storage and send the link to that data file in the message.

[Next &raquo;](200_services.html)