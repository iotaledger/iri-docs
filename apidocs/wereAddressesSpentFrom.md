
# [wereAddressesSpentFrom](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L533)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) wereAddressesSpentFromStatement(List<String> addresses)

Check if a list of addresses was ever spent from, in the current epoch, or in previous epochs.  If an address has a pending transaction, it is also marked as spend.

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
| addresses | List<String> | Required | List of addresses to check if they were ever spent from. |

## Responses

If successful, this method returns a `200 OK` response code and [WereAddressesSpentFrom](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/WereAddressesSpentFrom.java) in the body.

| Return type | Description |
|--|--|
| Integer duration | The duration it took to process this command in milliseconds |
| boolean[] states | States of the specified addresses in Boolean  Order of booleans is equal to order of the supplied addresses. |

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
"command": "wereAddressesSpentFrom", 
"addresses": ["JDLNPFJXBTQIKFNCQJDDIFLSIJPPUTBOAUQBWRRFRMQHGFMZCEKVJBKFHDJSINLJDRPK9H9ANWVEKKDA9VJOGMGBFMEGLXQMAVXDQEJUY9SXWKWYT9FEKQDO9RTTSDJCVHUXKLLQLZQEGXEBGLKSOAICBYRRQOVVTA", "VQMNGENVJLOXXWLDBMAYJNRTRZVOLVWFDJXFEZBJFRRVENOIVG9HXV9KDEJGGZBLJJCBQBAZGRMASRBZVCLOOVNTVJWNZFKJAB99THHOSPWAYKHQZ9KMPFKBQNJRQERV9NAVVEQHX9FPCWQTCS9GBICPWZRXGKZBOQ"]}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"duration": "733", "states": ["false", "false"]}
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
  "error": "COMMAND wereAddressesSpentFrom is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
