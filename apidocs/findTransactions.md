
# [findTransactions](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L1188)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) findTransactionsStatement(Map<String, Object> request)

  Find the transactions which match the specified input and return.  All input values are lists, for which a list of return values (transaction hashes), in the same order, is returned for all individual elements.  The input fields can either be `bundles`, `addresses`, `tags` or `approvees`.      Using multiple of these input fields returns the intersection of the values.  Returns an [ErrorResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/ErrorResponse.java) if more than maxFindTxs was found.

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
| request | Map<String, Object> | Required | The map with input fields                 Must contain at least one of 'bundles', 'addresses', 'tags' or 'approvees'. |

## Responses

If successful, this method returns a `200 OK` response code and [FindTransactionsResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/FindTransactionsResponse.java) in the body.

| Return type | Description |
|--|--|
| Integer duration | The duration it took to process this command in milliseconds |
| String[] hashes | The transaction hashes which are returned depend on your input.   For each specified input value, the command will return the following:    * `bundles`: returns the list of transactions which contain the specified bundle hash.<br/>  * `addresses`: returns the list of transactions which have the specified address as an input/output field.<br/>  * `tags`: returns the list of transactions which contain the specified tag value.<br/>  * `approvees`: returns the list of transactions which reference (i.e. approve) the specified transaction.<br/>   |

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
"command": "findTransactions", 
"request": ["DGJGKEBWWUTZJOGOJSUKQLYWNQDDJLLGBTMBOGXAERJLLOEUCI9KELTOWIJ9EAHDD9BFGDFBGSSFSLOGV", "LDMIKNOSJLORITEBBLFQLHWBVGTNXOXJNRQH9LGBGSPKHPAFHRYHCKKUHVOLTSLSS9GLJNLBIQRZSYVVS"]}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"duration": "933", "hashes": ["ZMBKZ9ITLRNXPTUFJSAFHKCMTLXIRGHQVQHSCTOKGQFOMPNNZJMOXJJKPPRLLB9LNKEMTFWNJAJLFKVWN", "JECGEOYUUPUQMYXEQZMASWJMLCJENUEXSRRVZJNK9LPXTKYY9LAEPUYHLVBKOEKQWAJQTEGPGXWVHANX9"]}
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
  "error": "COMMAND findTransactions is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
