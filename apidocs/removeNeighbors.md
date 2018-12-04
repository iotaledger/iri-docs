
# [removeNeighbors](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L749)
 [AbstractResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/AbstractResponse.java) removeNeighborsStatement(List<String> uris)

Temporarily removes a list of neighbors from your node.  The added neighbors will be added again after relaunching IRI.  Remove the neighbors from your config file or make sure you don't supply them in the -n command line option if you want to keep them removed after restart.   The URI (Unique Resource Identification) for removing neighbors is:  **udp://IPADDRESS:PORT**   Returns an [ErrorResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/ErrorResponse.java) if the URI scheme is wrong

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
| uris | List<String> | Required | The URIs of the neighbors we want to remove. |

## Responses

If successful, this method returns a `200 OK` response code and [RemoveNeighborsResponse](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/dto/RemoveNeighborsResponse.java) in the body.

| Return type | Description |
|--|--|
| Integer duration | The duration it took to process this command in milliseconds |
| int removedNeighbors | The amount of temporarily removed neighbors from this node.  Can be 0 or more. |

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
"command": "removeNeighbors", 
"uris": ["udp://8.8.8.8:14265", "udp://8.8.8.8:14265"]}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"duration": "621", "removedNeighbors": "442"}
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
  "error": "COMMAND removeNeighbors is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
