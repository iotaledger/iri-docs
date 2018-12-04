
# [getNodeInfo](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L965)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) getNodeInfoStatement()

Returns information about this node.

> **Important note:** This API is currently in Beta and is subject to change. Use of these APIs in production applications is not supported.

## Request

## Request headers

| Header       | Value | Required or Optional |
|:---------------|:--------|:--------|
| X-IOTA-API-Version | 1 | Required |
| Content-Type | application/json | Optional |
| Authorization  | Bearer {token} | Optional  |

## Responses

If successful, this method returns a `200 OK` response code and [GetNodeInfoResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNodeInfoResponse.java) in the body.

| Return type | Description |
|--|--|
| Integer duration | The duration it took to process this command in milliseconds |
| String appName | Name of the IOTA software you're currently using. (IRI stands for IOTA Reference Implementation) |
| String appVersion | The version of the IOTA software this node is running. |
| int jreAvailableProcessors | Available cores for JRE on this node. |
| long jreFreeMemory | The amount of free memory in the Java Virtual Machine. |
| String jreVersion | The JRE version this node runs on |
| long jreMaxMemory | The maximum amount of memory that the Java virtual machine will attempt to use. |
| long jreTotalMemory | The total amount of memory in the Java virtual machine. |
| String latestMilestone | The hash of the latest transaction that was signed off by the coordinator. |
| int latestMilestoneIndex | Index of the [latestMilestone](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNodeInfoResponse.java#L53) |
| String latestSolidSubtangleMilestone | The hash of the latest transaction which is solid and is used for sending transactions.   For a milestone to become solid, your local node must approve the subtangle of coordinator-approved transactions,    and have a consistent view of all referenced transactions. |
| int latestSolidSubtangleMilestoneIndex | Index of the [latestSolidSubtangleMilestone](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNodeInfoResponse.java#L65) |
| int milestoneStartIndex | The start index of the milestones.   This index is encoded in each milestone transaction by the coordinator |
| int neighbors | Number of neighbors this node is directly connected with. |
| int packetsQueueSize | The amount of transaction packets which are currently waiting to be broadcast. |
| long time | The difference, measured in milliseconds, between the current time and midnight, January 1, 1970 UTC |
| int tips | Number of tips in the network. |
| int transactionsToRequest | When a node receives a transaction from one of its neighbors,   this transaction is referencing two other transactions t1 and t2 (trunk and branch transaction).   If either t1 or t2 (or both) is not in the node's local database,   then the transaction hash of t1 (or t2 or both) is added to the queue of the "transactions to request".  At some point, the node will process this queue and ask for details about transactions in the   "transaction to request" queue from one of its neighbors.   This number represents the amount of "transaction to request" |
| String[] features | Every node can have features enabled or disabled.   This list will contain all the names of the features of a node as specified in [Feature](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/Feature.java). |
| String coordinatorAddress | The address of the Coordinator being followed by this node. |

## Example  

### Request

The following is an example of the request.

 ## Example
 
 ```bash
 curl http://localhost:14265 
-X POST 
-H 'Content-Type: application/json' 
-H 'X-IOTA-API-Version: 1' 
-d '{ 
"command": "getNodeInfo", 
}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"duration": "239", "appName": "appname", "appVersion": "appversion", "jreAvailableProcessors": "670", "jreFreeMemory": "3G", "jreVersion": "jreversion", "jreMaxMemory": "2G", "jreTotalMemory": "2G", "latestMilestone": "ASZUFGCDBIC9FJTRXNZACRFIJCBF9SILXMSZN9UATUWWKVVLGCMBCOYXIOOOKKHMDUZKZUFJISKLXHQXFFYCWETBPTFDITLDHZKLINPIENYWLNUUPKIJTUVFUDXTTGMNSUOJAMJJPNKLLMEOIGHLPQESEFLEKQJ9GV", "latestMilestoneIndex": "737", "latestSolidSubtangleMilestone": "XTWXVHHJYL9LSODZKPMDSUZNPUVWYTRQGJEHUWNSBWHMHSKGWYQAQI9FVMDBLNBZTEDLMFPFQCVFFWFFDDNAYZDMCQBSUETXTPQTWESTRCWJJEEBQSTLUDIWNAXRMTBJTCGIZQGKVAPESMEDTAVAIRBKAAKVZSUZQK", "latestSolidSubtangleMilestoneIndex": "326", "milestoneStartIndex": "656", "neighbors": "670", "packetsQueueSize": "680", "time": "time", "tips": "501", "transactionsToRequest": "875", "features": ["features", "features"], "coordinatorAddress": "MJDHGYVFAJGCLYVTYUXKGU9FTVPSTSAKUGDZSKSVWZPVORANHMJKVIBMYSNTCJOLAGQDHSYKWHRCS9SCZWIIYHWECTRGQXKTRCNKQABZXKYPHHJVGSGPMGZQVEEW9DZPOHPVLNBZSFIBFJWDQPUZTMARYTPLPQOHNU"}
```

### Response - 400

A node returns this for various reasons. These are the most common ones:
* Invalid API Version
* The maximal number of characters the body of an API call is exceeded
* The command contains invalid parameters

```json
{
  "duration": 15,
  "error": "Error specific information"
}
```

### Response - 401

```json
{
  "duration": 15,
  "error": "COMMAND getNodeInfo is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
