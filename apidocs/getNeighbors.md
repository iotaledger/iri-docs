
# [getNeighbors](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L701)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) getNeighborsStatement()

Returns the set of neighbors you are connected with, as well as their activity statistics (or counters).  The activity counters are reset after restarting IRI.

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
| [GetNeighborsResponse.Neighbor[]](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetNeighborsResponse/Neighbor.java) neighbors | The neighbors you are connected with, as well as their activity counters.<br/>**address**: The address of your neighbor<br/>**numberOfAllTransactions**: Number of all transactions sent (invalid, valid, already-seen)<br/>**numberOfRandomTransactionRequests**: Random tip requests which were sent<br/>**numberOfNewTransactions**: New transactions which were transmitted.<br/>**numberOfInvalidTransactions**: Invalid transactions your neighbor has sent you.   These are transactions with invalid signatures or overall schema.<br/>**numberOfStaleTransactions**: Stale transactions your neighbor has sent you.  These are transactions with a timestamp older than your latest snapshot.<br/>**numberOfSentTransactions**: Amount of transactions send through your neighbor<br/>**connectionType**: The method type your neighbor is using to connect (TCP / UDP) |

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
{"duration": "771", "neighbors": ["{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 231, 
"numberOfRandomTransactionRequests": 738 
"numberOfNewTransactions": 63 
"numberOfInvalidTransactions": 677, 
"numberOfStaleTransactions": 443 
"numberOfSentTransactions": 793 
"connectiontype": TCP 
}", "{ 
"address": "/8.8.8.8:14265", 
"numberOfAllTransactions": 198, 
"numberOfRandomTransactionRequests": 965 
"numberOfNewTransactions": 116 
"numberOfInvalidTransactions": 337, 
"numberOfStaleTransactions": 817 
"numberOfSentTransactions": 278 
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
