
# [getTransactionsToApprove](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L841)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) getTransactionsToApproveStatement(int depth, Optional<[Hash](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/model/Hash.java)> reference)

Tip selection which returns `trunkTransaction` and `branchTransaction`. The input value `depth` determines how many milestones to go back for finding the transactions to approve. The higher your `depth` value, the more work you have to do as you are confirming more transactions. If the `depth` is too large (usually above 15, it depends on the node's configuration) an error will be returned. The `reference` is an optional hash of a transaction you want to approve. If it can't be found at the specified `depth` then an error will be returned.

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
| depth | int | Required | Number of bundles to go back to determine the transactions for approval. |
| reference | Optional<[Hash](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/model/Hash.java)> | Optional | Hash of transaction to start random-walk from, used to make sure the tips returned reference a given transaction in their past. |

## Responses

If successful, this method returns a `200 OK` response code and [GetTransactionsToApproveResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetTransactionsToApproveResponse.java) in the body.

| Return type | Description |
|--|--|
| Integer duration | The duration it took to process this command in milliseconds |
| String branchTransaction | The branch transaction tip to reference in your transaction or bundle |
| String trunkTransaction | The trunk transaction tip to reference in your transaction or bundle |

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
"command": "getTransactionsToApprove", 
"depth": "15", "reference": ["X9CMNUW9VGMIAS9STZBILGQLELAAIJOCUTYHYGVYSKEVYTEOZBHRUXE9GLUBXZTCHKGWON9IFX9RTJHMO", "VZWLUHRXWK9RLKLQYGEUGFVY9KADYWANKCWOFFRMHPSLCHMDYFVEKQZJQPCHISHFWXVHSHAOPKIBNSNKN"]}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"duration": "457", "branchTransaction": "LUJRVNSDLHSDCX9MVSBZFWZHVRDXRDKZTOTRFMGKSMZGZZUFRFOUHNFC9HZMWQHYONGMOWBMUVEFRADOS", "trunkTransaction": "CENBHDNCWLFDKSYZUTR9TZBMTANCGGGJJWE9M9JIWZKXELGVZSZSPFITXJUKF9PYKYSCQEWEAXMUMQMHH"}
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
  "error": "COMMAND getTransactionsToApprove is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
