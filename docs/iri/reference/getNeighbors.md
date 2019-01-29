
# [getNeighbors](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L701)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) getNeighborsStatement()

Returns the set of neighbors you are connected with, as well as their activity statistics (or counters). The activity counters are reset after restarting IRI.

> **Important note:** This API is currently in Beta and is subject to change. Use of these APIs in production applications is not supported.

## Request

## Request headers

| Header       | Value | Required or Optional |
|:---------------|:--------|:--------|
| X-IOTA-API-Version | 1 | Required |
| Content-Type | application/json | Optional |
| Authorization  | Bearer {token} | Optional  |

## Responses

If successful, this method returns a `200 OK` response code and [GetNeighborsResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNeighborsResponse.java) in the body.

| Return type | Description |
|--|--|
| Integer duration | The duration it took to process this command in milliseconds |
| [GetNeighborsResponse.Neighbor[]](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNeighborsResponse/Neighbor.java) neighbors | The neighbors you are connected with, as well as their activity counters.**address**: The address of your neighbor**numberOfAllTransactions**: [numberOfAllTransactions](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNeighborsResponse/Neighbor.java#L61)**numberOfNewTransactions**: [numberOfNewTransactions](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNeighborsResponse/Neighbor.java#L71)**numberOfInvalidTransactions**: [numberOfInvalidTransactions](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNeighborsResponse/Neighbor.java#L77)**numberOfStaleTransactions**: [numberOfStaleTransactions](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNeighborsResponse/Neighbor.java#L83)**numberOfSentTransactions**: [numberOfSentTransactions](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNeighborsResponse/Neighbor.java#L88)**numberOfRandomTransactionRequests**: [numberOfRandomTransactionRequests](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNeighborsResponse/Neighbor.java#L66)**connectionType**: [connectionType](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNeighborsResponse/Neighbor.java#L93) |

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
"command": "getNeighbors", 
}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"duration": "53", "neighbors": ["{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 158, 
"numberOfRandomTransactionRequests": 271 
"numberOfNewTransactions": 956 
"numberOfInvalidTransactions": 539, 
"numberOfStaleTransactions": 663 
"numberOfSentTransactions": 672 
"connectiontype": TCP 
}", "{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 105, 
"numberOfRandomTransactionRequests": 644 
"numberOfNewTransactions": 745 
"numberOfInvalidTransactions": 418, 
"numberOfStaleTransactions": 450 
"numberOfSentTransactions": 906 
"connectiontype": UDP 
}"]}
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
  "error": "COMMAND getNeighbors is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
