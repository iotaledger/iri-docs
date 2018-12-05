
# [getTrytes](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L773)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) getTrytesStatement(List<String> hashes)

Returns the raw transaction data (trytes) of a specific transaction.  These trytes can then be easily converted into the actual transaction object.  See utility and [Transaction](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/model/persistables/Transaction.java) functions in an IOTA library for more details.

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
| hashes | List<String> | Required | The transaction hashes you want to get trytes from. |

## Responses

If successful, this method returns a `200 OK` response code and [GetTrytesResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetTrytesResponse.java) in the body.

| Return type | Description |
|--|--|
| Integer duration | The duration it took to process this command in milliseconds |
| String[] trytes | The raw transaction data (trytes) of the specified transactions.  These trytes can then be easily converted into the actual transaction object.   See library functions as to how to transform back to a [Transaction](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/model/persistables/Transaction.java). |

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
"command": "getTrytes", 
"hashes": ["BIUZIDHKCEHM9IYB9LMMLMJVVNZTFQDLUKIETXLPSTZLBGMIEHCMUITXMSXCUTN9RXNUDLEZ9HRDL9BHE", "WAQRYLLJFWZMHJDSDQQOCDBHZUHQEITWJHYXGJORQBYUSRFYLVXV9W9BRTACOCKSHRHVIUFLHBBOLJNHQ"]}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"duration": "817", "trytes": ["NAYXOPCOKUPIHSLRGXXQHTUVX99OY9YRAYI9ZFLOMOCUC9RYGOXMGFCU9XGILU9YRYCNOEKIGGPVVESKZRWGHQYWRYQCPKXKZAJNPNARMXDDTDGLNQUNIRNOAMVAJGYUGBYKSBFUU9BUHC9OCGSTZCJNCSQZPACYBZ", "UXUD9IYVRPSJYGCXVQBIIBSCI9AWGDCHUKSVPXMZMXLIVFWMZIITPXRRLLDBGQKB9ZXWPSPIOSXA9XJSSJSXDGDKLVIOLAAQBDINAXDZUYQUPZUBJH9S9HJHLKWZNQKBDW9ZCDGNYRL9C99ZWPXMIDSLAUWTGPECID"]}
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
  "error": "COMMAND getTrytes is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
