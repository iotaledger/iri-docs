
# [getTips](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L907)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) getTipsStatement()

Returns all tips currently known by this node.

> **Important note:** This API is currently in Beta and is subject to change. Use of these APIs in production applications is not supported.

## Request

## Request headers

| Header       | Value | Required or Optional |
|:---------------|:--------|:--------|
| X-IOTA-API-Version | 1 | Required |
| Content-Type | application/json | Optional |
| Authorization  | Bearer {token} | Optional  |

## Responses

If successful, this method returns a `200 OK` response code and [GetTipsResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/GetTipsResponse.java) in the body.

| Return type | Description |
|--|--|
| Integer duration | The duration it took to process this command in milliseconds |
| String[] hashes | The current tips as seen by this node. |

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
"command": "getTips", 
}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"duration": "46", "hashes": ["EBRVUFVWGPBXHSNZGEZO9MEKVEEBCHQZRIMCHSZMH9BYYGMIPW9TCMCYUUPZLFMLOGXGKFHGPXYLGDQZL", "NJOOFTIRYWGZ9FYOVGPUTKKVNMEHYBR9RHUZVFKNPZHMQPAYRQQMOXLIAZX99IUCMHCGY9MYLTGMLVHAR"]}
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
  "error": "COMMAND getTips is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
