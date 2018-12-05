
# [broadcastTransactions](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L1331)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) broadcastTransactionsStatement(List<String> trytes)

Broadcast a list of transactions to all neighbors.  The trytes to be used for this call should be valid, attached transaction trytes.  These trytes are returned by `attachToTangle`, or by doing proof of work somewhere else.

> **Important note:** This API is currently in Beta and is subject to change. Use of these APIs in production applications is not supported.

## Request

## Request headers

| Header       | Value | Required or Optional |
|:---------------|:--------|:--------|
| X-IOTA-API-Version | 1 | Required |
| Content-Type | application/json | Optional |
| Authorization  | Bearer {token} | Optional  |

## Request parameters
| Parameter       | Type | Required or Optional | Description |
|:---------------|:--------|:--------| :--------|
| trytes | List<String> | Required | The list of transaction trytes to broadcast |

## Responses

If successful, this method returns a `200 OK` response code and [AbstractResponse.Emptyness](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse/Emptyness.java) in the body.

| Return type | Description |
|--|--|
| Integer duration | The duration it took to process this command in milliseconds |

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
"command": "broadcastTransactions", 
"trytes": ["NWRCRHCQLQXQRCFRJLI9IDJIESSQGOMXYPOQINCBWTHEJMVWTCR9TYYGBFPKYJBBKSB9JTOGSKJLLQROYQKSU9CHEXAISLRKNYDCEDLUYSGRROMYPTZVSMIKPFFJCNFDQZHITVARJZUFLSODDVXHJUY9DNYLZUYVEW", "FODAPHLSAVGTZKWPUNMKZLURHCRVOE9GELLKHYDKMPRXIGSHKNBBMUJANGDZXPSDTCLYYBAQ9EOQRAKTZYRFQJRTULFYGYRXCYPXPXJY9HTTZXEWM9EDKZCBNTTEQCAJJCKWD9FBZCYGRHGRQRYJVGELNNKDHPGYKM"]}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"duration": "496"}
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
  "error": "COMMAND broadcastTransactions is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
