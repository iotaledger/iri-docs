
# [checkConsistency](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L636)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) checkConsistencyStatement(List<String> transactionsList)

Checks the consistency of the transactions.  Marks state as false on the following checks:    * Missing a reference transaction<br/>  * Invalid bundle<br/>  * Tails of tails are invalid<br/>      If a transaction does not exist, or it is not a tail, an [ErrorResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/ErrorResponse.java) is returned.

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
| transactionsList | List<String> | Required | Transactions you want to check the consistency for |

## Responses

If successful, this method returns a `200 OK` response code and [CheckConsistency](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/CheckConsistency.java) in the body.

| Return type | Description |
|--|--|
| Integer duration | The duration it took to process this command in milliseconds |
| boolean state | The state of all the provided tails, which is set to  on the following checks<br/>    * Missing a reference transaction<br/>  * Invalid bundle<br/>  * Tails of tails are invalid<br/>   |
| String info | If state is , this provides information on the cause of the inconsistency. |

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
"command": "checkConsistency", 
"transactionsList": ["OLQXVJKG9ROKALQOGJIAFVLEWGLJPEPXDEEUWJVXEPDPDZPYMGAPSHBWLDFG9JFGGTRJOOXSVNJZFRGVK", "CHTRAHOGLFDXALMSF9QGXJQDXHZPJTTDZEKWAUCQA9AUBEGII9GQLVCYY9MJVQZFZA9S9CXCZQA9GGVHV"]}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"duration": "975", "state": "false", "info": "LPBFOQGEPNRPRVXMYQWWKAAV9MLKBZNKIOAEVCMJGZVIJOTOYCHN9BDTTRDRSELYROUI9UOFXJPMJEDFX"}
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
  "error": "COMMAND checkConsistency is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
