
# [getBalances](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L1370)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) getBalancesStatement(List<String> addresses, List<String> tips, int threshold)

  Calculates the confirmed balance, as viewed by the specified `tips`.   If you do not specify the referencing `tips`,   the returned balance is based on the latest confirmed milestone.  In addition to the balances, it also returns the referencing `tips` (or milestone),   as well as the index with which the confirmed balance was determined.  The balances are returned as a list in the same order as the addresses were provided as input.    Returns an [ErrorResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/ErrorResponse.java) if tips are not found, inconsistent or the threshold is invalid.

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
| addresses | List<String> | Required | The addresses where we will find the balance for. |
| tips | List<String> | Required | The optional tips to find the balance through. |
| threshold | int | Required | The confirmation threshold between 0 and 100(inclusive).                    Should be set to 100 for getting balance by counting only confirmed transactions. |

## Responses

If successful, this method returns a `200 OK` response code and [GetBalancesResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetBalancesResponse.java) in the body.

| Return type | Description |
|--|--|
| Integer duration | The duration it took to process this command in milliseconds |
| List<String> balances | The balances as a list in the same order as the addresses were provided as input |
| List<String> references | The tips used to view the balances. If none were supplied this will be the latest confirmed milestone. |
| int milestoneIndex | The milestone index with which the confirmed balance was determined |

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
"command": "getBalances", 
"addresses": ["XJBOCKENYQEIQGMIUGLEIOOLEWHKHNUBHEFJSZCXCJYZHKDJQTNIZXWFAIEVWCDDKYGUUBRNMAFKNDONBNLAHFUCKWDBFLAOPQOXCYPGAIQPHNTVIIGCWBWSVYBXKYCT9KAKMMUX9NMAVJZKVYWATSQHRNKQGIHFZI", "TTJ9ZVPOHTHROELJUAOLNEOLJCZEEGISPRCWBENWVNOY9IOKFJJT9OLEQRADCUP9MYOZBQAJQZH9CZJTGVRF9XRUTDSIO9XDEIWKASKWXDOGOCIQSNLWTSKMTADFDBUYRFLWWSSKRWXRBEMJTLDRZALGBOXJRXITQO"], "tips": ["DIUMVBXKBFSFHNBINLHP9ENB9MDILNVODEOYLEHNCMYCSSQIRHBNFUDPEQUWU9NJLJAZEOAPNQN9XVHGQ", "IXMKKU9YHWYF9KFFLIFOYTSJDPQLBE9CUMDILFAYYYHQKKIZMPTWYRWFXZEAJYKODXYGJEOVYGLWQNLZA"], "threshold": "100"}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"duration": "489", "balances": ["QBVHEAGRJQGRTL9AETF9RUGWCVSGTUASKDHZURMPJBAOIDHXPPKDBOFMGAJUFDKQRDYJVZMMNUNDVXCPL", "XUUIVMKQKHGBUKGSQFNYAWYAJLNSAPSBAHRMBRXZDMBTUXMOKCTMOLJSCMRUW9SD9HGTHJHSOQSK9NCCP"], "references": ["QFJEULLXM9UTDZFAGOPKMUUGDNQBLXAGUKUG9QTXBX9GEZUFBEZMBXT9HWLQLPUCJYTYWJKELMQDNAXKY", "TMDFCCKOERJZRMSA9OWGHFLTSDOLUROHNUKYRB9VNWIWJDKLTSF9LTYZUYGYEJJHZTYVJGYIQIXVXPRBK"], "milestoneIndex": "879"}
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
  "error": "COMMAND getBalances is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
