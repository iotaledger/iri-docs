
---
### [getNeighbors](https://github.com/iotaledger/iri/blob/dev/src/main/java/com/iota/iri/service/API.java#L708)
 [AbstractResponse](/javadoc/com/iota/iri/service/dto/abstractresponse/) getNeighborsStatement()

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
{"duration": "66", "neighbors": ["{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 848, 
"numberOfInvalidTransactions": 240, 
"numberOfNewTransactions": 444 
}", "{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 339, 
"numberOfInvalidTransactions": 544, 
"numberOfNewTransactions": 211 
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
{"duration": "17", "neighbors": ["{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 335, 
"numberOfInvalidTransactions": 917, 
"numberOfNewTransactions": 965 
}", "{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 360, 
"numberOfInvalidTransactions": 599, 
"numberOfNewTransactions": 373 
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
{"duration": "3", "neighbors": ["{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 920, 
"numberOfInvalidTransactions": 949, 
"numberOfNewTransactions": 364 
}", "{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 214, 
"numberOfInvalidTransactions": 650, 
"numberOfNewTransactions": 854 
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

Returns [GetNeighborsResponse](/javadoc/com/iota/iri/service/dto/getneighborsresponse/)

|Return | Description |
|--|--|
| duration | The duration it took to process this command in milliseconds |
| neighbors | The list of neighbors, including the following stats: address, connectionType, numberOfAllTransactions, numberOfRandomTransactionRequests, numberOfNewTransactions, numberOfInvalidTransactions, numberOfSentTransactions |
***