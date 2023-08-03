# API Endpoint

Endpoint Base Url: <mark style="color:yellow;">`https://api.sobal.fi`</mark>

Supported chain Ids:&#x20;

| ChainId   | Network Name | Type    |
| --------- | ------------ | ------- |
| 8453      | Base         | Mainnet |
| 245022934 | Neon         | Mainnet |
| 84531     | Base Goerli  | Testnet |
| 245022926 | Neon Devnet  | Testnet |

`{chainId}` in each endpoint is the chain/network number (refer to the table above) you wish to request from.

`{id}` is a specific pool id within the chain.

* `/graphql` - GraphQL endpoint for retrieving pools with filters / queries. Forwards requests to Appsync. See 'GraphQL Requests' section for more info.
* `/pools/{chainId}/update` - Runs the worker lambda that fetches the latest pool information from the graph and saves it in the database.
* `/pools/{chainId}` - Returns a JSON array of all Balancer pools of that chain
* `/pools/{chainId}/{id}` - Returns JSON information about a pool of a specific `id`.
* `/sor/{chainId}` - Run a SOR (Smart Order Router) query against the balancer pools and returns [SerializedSwapInfo](https://github.com/Sobal/balancer-api/blob/master/src/modules/sor/types.ts).
* `/order/{chainId}` - Run a SOR (Smart Order Router) query against the balancer pools and returns a [SorOrderResponse](https://github.com/Sobal/balancer-api/blob/master/src/modules/sor/types.ts).
* `/tokens/{chainId}` - Returns a JSON array of all known tokens of that chain



\


\
