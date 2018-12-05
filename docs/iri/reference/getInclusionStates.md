
# [getInclusionStates](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L1004)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) getInclusionStatesStatement(List<String> transactions, List<String> tips)

  Get the inclusion states of a set of transactions.  This is for determining if a transaction was accepted and confirmed by the network or not.  You can search for multiple tips (and thus, milestones) to get past inclusion states of transactions.      This API call returns a list of boolean values in the same order as the submitted transactions.<br/>  Boolean values will be `true` for confirmed transactions, otherwise `false`.    Returns an [ErrorResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/ErrorResponse.java) if a tip is missing or the subtangle is not solid

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
| transactions | List<String> | Required | List of transactions you want to get the inclusion state for. |
| tips | List<String> | Required | List of tips (including milestones) you want to search for the inclusion state. |

## Responses

If successful, this method returns a `200 OK` response code and [GetInclusionStatesResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetInclusionStatesResponse.java) in the body.

| Return type | Description |
|--|--|
| Integer duration | The duration it took to process this command in milliseconds |
| boolean[] states | A list of booleans indicating if the transaction is confirmed or not, according to the tips supplied.  Order of booleans is equal to order of the supplied transactions. |

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
"command": "getInclusionStates", 
"transactions": ["ZIKICDTSIDVHXXHZLFPMOPQIIDOYMNJRZMOWKXRMNVVQYGBJVNVKZNFUUWD9EQHBIGGUMQRHOMCNXXLQZ", "YYJUIDHEWFLBZIXGRFHSATZOZENIQWFSYVJD9BQJGOCALNUACTPALIJADYSPFMHTRKZQXBSAQIMRUFLSF"], "tips": ["CWDP9DBWDPREIKKTCSELTMHDQFJIE9OLQI9TJEIWVJPGYCGXEZYF9BGQVPKQDYJQQIRCDXBLDCHJOJLVO", "FGRKWAKWOHVTMPJ9DECZFYKUGBWDH9EMLOGVZBKLISJMB9AYTISXZ9KQDCBL9NOYXOKQSRMXFUSALHC9Y"]}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"duration": "561", "states": ["false", "false"]}
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
  "error": "COMMAND getInclusionStates is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
