
---
### [getNodeInfo](https://github.com/iotaledger/iri/blob/dev/src/main/java/com/iota/iri/service/API.java#L727)
 [AbstractResponse](/javadoc/com/iota/iri/service/dto/abstractresponse/) getNodeInfoStatement()

Returns information about your node.

<Tabs> 

<Tab language="Python">

<Section type="request">
```Python
import urllib2
import json

command = {"command": "getNodeInfo"}

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
{"duration": "522", "appName": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "appVersion": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "jreAvailableProcessors": "180", "jreFreeMemory": "missing_data", "jreMaxMemory": "missing_data", "jreTotalMemory": "missing_data", "jreVersion": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "latestMilestone": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "latestMilestoneIndex": "775", "latestSolidSubtangleMilestone": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "latestSolidSubtangleMilestoneIndex": "53", "milestoneStartIndex": "576", "neighbors": "32", "packetsQueueSize": "688", "time": "missing_data", "tips": "248", "transactionsToRequest": "318"}
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

var command = {"command": "getNodeInfo"}

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
{"duration": "28", "appName": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "appVersion": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "jreAvailableProcessors": "143", "jreFreeMemory": "missing_data", "jreMaxMemory": "missing_data", "jreTotalMemory": "missing_data", "jreVersion": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "latestMilestone": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "latestMilestoneIndex": "523", "latestSolidSubtangleMilestone": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "latestSolidSubtangleMilestoneIndex": "252", "milestoneStartIndex": "222", "neighbors": "167", "packetsQueueSize": "816", "time": "missing_data", "tips": "681", "transactionsToRequest": "428"}
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
-d '{"command": "getNodeInfo"}'
```
</Section>

<Section type="response">
```json
{"duration": "339", "appName": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "appVersion": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "jreAvailableProcessors": "745", "jreFreeMemory": "missing_data", "jreMaxMemory": "missing_data", "jreTotalMemory": "missing_data", "jreVersion": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "latestMilestone": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "latestMilestoneIndex": "487", "latestSolidSubtangleMilestone": "P9KFSJVGSPLXAEBJSHWFZLGP9GGJTIO9YITDEHATDTGAFLPLBZ9FOFWWTKMAZXZHFGQHUOXLXUALY9999", "latestSolidSubtangleMilestoneIndex": "944", "milestoneStartIndex": "153", "neighbors": "594", "packetsQueueSize": "573", "time": "missing_data", "tips": "269", "transactionsToRequest": "765"}
```
</Section>

<Section type="error">
```json
{"error": "'command' parameter has not been specified"}
```
</Section>
</Tabs<





***

Returns [GetNodeInfoResponse](/javadoc/com/iota/iri/service/dto/getnodeinforesponse/)

|Return | Description |
|--|--|
| duration | The duration it took to process this command in milliseconds |
| appName | Gets the app name |
| appVersion | Name of the IOTA software you're currently using (IRI stands for Initial Reference Implementation) |
| jreAvailableProcessors | Available cores on your machine for JRE. |
| jreFreeMemory | The amount of free memory in the Java Virtual Machine. |
| jreMaxMemory | The maximum amount of memory that the Java virtual machine will attempt to use. |
| jreTotalMemory | The total amount of memory in the Java virtual machine. |
| jreVersion | The JRE version this node runs on |
| latestMilestone | The hash of the latest transaction that was signed off by the coordinator. |
| latestMilestoneIndex | Index of the latest milestone. |
| latestSolidSubtangleMilestone | The hash of the latest transaction which is solid and is used for sending transactions. For a milestone to become solid your local node must basically approve the subtangle of coordinator-approved transactions, and have a consistent view of all referenced transactions. |
| latestSolidSubtangleMilestoneIndex | Index of the latest solid subtangle. |
| milestoneStartIndex | Gets the start milestone index |
| neighbors | Number of neighbors you are directly connected with. |
| packetsQueueSize | Packets which are currently queued up. |
| time | Current UNIX timestamp. |
| tips | Number of tips in the network. |
| transactionsToRequest | When a node receives a transaction from one of its neighbors, this transaction is referencing two other transactions t1 and t2 (trunk and branch transaction). If either t1 or t2 (or both) is not in the node's local database, then the transaction hash of t1 (or t2 or both) is added to the queue of the "transactions to request". At some point, the node will process this queue and ask for details about transactions in the "transaction to request" queue from one of its neighbors. By this means, nodes solidify their view of the tangle (i.e. filling in the unknown parts). |
***