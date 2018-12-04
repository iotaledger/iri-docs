
# [attachToTangle](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/service/API.java#L1508)
 List<String> attachToTangleStatement([Hash](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/model/Hash.java) trunkTransaction, [Hash](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/model/Hash.java) branchTransaction, int minWeightMagnitude, List<String> trytes)

  Prepares the specified transactions (trytes) for attachment to the Tangle by doing Proof of Work.  You need to supply `branchTransaction` as well as `trunkTransaction`.  These are the tips which you're going to validate and reference with this transaction.   These are obtainable by the `getTransactionsToApprove` API call.      The returned value is a different set of tryte values which you can input into   `broadcastTransactions` and `storeTransactions`.  The last 243 trytes of the return value consist of the following:    * `trunkTransaction`<br/>  * `branchTransaction`<br/>  * `nonce`<br/>      These are valid trytes which are then accepted by the network.

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
| trunkTransaction | [Hash](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/model/Hash.java) | Required | A reference to an external transaction (tip) used as trunk.                          The transaction with index 0 will have this tip in its trunk.                          All other transactions reference the previous transaction in the bundle (Their index-1). |
| branchTransaction | [Hash](https://github.com/iotaledger/iri/blob/master/src/main/java/com/iota/iri/model/Hash.java) | Required | A reference to an external transaction (tip) used as branch.                           Each Transaction in the bundle will have this tip as their branch, except the last.                           The last one will have the branch in its trunk. |
| minWeightMagnitude | int | Required | The amount of work we should do to confirm this transaction.                             Each 0-trit on the end of the transaction represents 1 magnitude.                             A 9-tryte represents 3 magnitudes, since a 9 is represented by 3 0-trits.                            Transactions with a different minWeightMagnitude are compatible. |
| trytes | List<String> | Required | The list of trytes to prepare for network attachment, by doing proof of work. |

## Responses

If successful, this method returns a `200 OK` response code and List in the body.

| Return type | Description |
|--|--|
| List<String> trytes | The list of transactions in trytes, ready to be broadcast to the network. |

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
"command": "attachToTangle", 
"trunkTransaction": "OMCJLQS9GIAYIHGDVKXIOTTCDSYLZSFBBRUHYLCYXMRUNKWGZH9NHZI9MI9XW9ED9OCFMCXVLLZVOCEFOJHHNTJBHAQ9ODUDSWZXWFFCHNJ9AGWPB9AXTCNVDZAODJANW9CLJS9E9XSDRYGOEWMDV9RKCAHSWPXAAH", "branchTransaction": "PRMCFLSSKWQUGQJEXIVDYEJUTSNQJKIMGKSR9WBDIUVUQZUKLIVENUIWZBEJXLGXXYYIAEGHZGTASTDASNDXHAHRCTVMPTLRMTJSHPLBAIWATARGIZENLYEMKXOEQBUNPEOIR9SPQTLRBUQBEKWUGSEDGYUINLXQKW", "minWeightMagnitude": "18", "trytes": ["PWCPWZCKBPMPSTXUXJXHNHGGXYJ9JE9HNMFYENEWLWJMFIEUCJMFCIQOGZPXZGFPLTNGWJHTA9DLSQDUUNIOKNQEGACRQWOLTYE9XCIFXRZBWLAGIKFNHJFNQKBXCGTOIXPOBTRMUFZWROHWJOHLMLFYRCYAUHDUGE", "X9I9ROCZPEISU9SNHLLBMMKVL9DFEMPOSFGH9A9KCIOKRYAASSJEFJYFPDTBIJP9VIHDCBFNWTBQLSIRKVCYBAKRMQD9ZMXAEHF9ZSEYBCE9ZLKTETAHPUGRRSWGCLFFUGFBQAUHDPUZRTUVWQKJAYYYIOZIBZHYRH"]}'
 ```

### Response - 200

The following is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{"trytes": ["CKNAJQATSJMPDEITZ9TYINLLBDIAQ9DADOWHUJSMCKTBE9ICCLFHFSGXDIGJJEDQSNTZU9HPWVF99WQQPZTETL9BNVIUTZYUMBCVJLPPGDGTPKGJGTFEN9YY9CZ9RIUTXCIUJIFOZHMGODQ9BUNZSEQZHJKLKKCHKP", "ZYYUEFFG9NDJSSVLCYKFEYWVWNDELHGIM9QMZQHXNQHAJUQCTQITJTDXUXGIJOHFIFCWPMGYDKODBFWGSXEMSK9SNDINNFHPZDPVPJOPTZKXFREJXMLIVEMCMBXASFSUEAJYMRLFDKTHYJI9ZDVXB9BFUHNMDAZFAZ"]}
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
  "error": "COMMAND attachToTangle is not available on this node"
}
```

### Response - 500

```json
{
  "duration": 15,
  "exception": "Internal server error message"
}
```
