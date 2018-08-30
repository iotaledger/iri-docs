
---
### [getNeighbors](https://github.com/iotaledger/iri/blob/dev/src/main/java/com/iota/iri/service/API.java#L708)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/dev/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) getNeighborsStatement()

Returns the set of neighbors you are connected with, as well as their activity statistics (or counters). 
 The activity counters are reset after restarting IRI.

<Tabs> 

<Tab language="Python">

<Section type="request">

```Python
import urllib2
import json

command = {"command": "getNeighbors"}

stringified = json.dumps(command)

headers = {
    'content-type': 'application/json',
    'X-IOTA-API-Version': '1'
}

request = urllib2.Request(url="http://localhost:14265", data=stringified, headers=headers)
returnData = urllib2.urlopen(request).read()

jsonData = json.loads(returnData)

print jsonData
```
</Section>

<Section type="response">

```json
{"duration": "71", "neighbors": ["{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 654, 
"numberOfInvalidTransactions": 249, 
"numberOfNewTransactions": 142 
}", "{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 570, 
"numberOfInvalidTransactions": 141, 
"numberOfNewTransactions": 256 
}"]}
```
</Section>

<Section type="error">

```json
{"error": "'command' parameter has not been specified"}
```
</Section>

<Tab language="NodeJS">

<Section type="request">

```javascript
var request = require('request');

var command = {"command": "getNeighbors"}

var options = {
  url: 'http://localhost:14265',
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
		'X-IOTA-API-Version': '1',
    'Content-Length': Buffer.byteLength(JSON.stringify(command))
  },
  json: command
};

request(options, function (error, response, data) {
  if (!error && response.statusCode == 200) {
    console.log(data);
  }
});
```
</Section>

<Section type="response">

```json
{"duration": "941", "neighbors": ["{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 889, 
"numberOfInvalidTransactions": 246, 
"numberOfNewTransactions": 835 
}", "{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 104, 
"numberOfInvalidTransactions": 512, 
"numberOfNewTransactions": 989 
}"]}
```
</Section>

<Section type="error">

```json
{"error": "'command' parameter has not been specified"}
```
</Section>

<Tab language="cURL">

<Section type="request">

```bash
curl http://localhost:14265 
-X POST 
-H 'Content-Type: application/json' 
-H 'X-IOTA-API-Version: 1' 
-d '{"command": "getNeighbors"}'
```
</Section>

<Section type="response">

```json
{"duration": "65", "neighbors": ["{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 401, 
"numberOfInvalidTransactions": 676, 
"numberOfNewTransactions": 7 
}", "{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 427, 
"numberOfInvalidTransactions": 811, 
"numberOfNewTransactions": 941 
}"]}
```
</Section>

<Section type="error">

```json
{"error": "'command' parameter has not been specified"}
```
</Section>
</Tabs<





***

Returns [GetNeighborsResponse](https://github.com/iotaledger/iri/blob/dev/src/main/java/com/iota/iri/service/dto/GetNeighborsResponse.java)

|Return | Description |
|--|--|
| duration | The duration it took to process this command in milliseconds |
| neighbors | The list of neighbors, including the following stats: address, connectionType, numberOfAllTransactions, numberOfRandomTransactionRequests, numberOfNewTransactions, numberOfInvalidTransactions, numberOfSentTransactions |
***