# Smart Order Router Queries

The Smart Order Router is a package that, for any given input and output token, finds you the best trade path across all Sobal pools. It is used by the Sobal frontend to calculate trades.

{% hint style="info" %}
Visit the [API Endpoint page](api-endpoint.md) to receive more data about the endpoints location and how to interact with it.
{% endhint %}

### Submitting requests

You can POST the following JSON content to the endpoints `/sor` or `/order` to return smart order router information.

```typoscript
{
    sellToken: string<Address>, # The address of the token you wish to sell
    buyToken: string<Address>, # The address of the token you wish to buy
    orderKind: string<buy|sell>, # Either 'buy' or 'sell', described further below
    amount: int, # The amount in sellToken or buyToken that you wish to sell/buy
    gasPrice: int, # The current gas price in wei, this is used to ensure your trade is most efficient considering the gas cost of performing multiple swaps.

    # The following are for /order only
    sender: string<Address>, # The address of the wallet sending sellToken.
    receiver: string<Address>, # The address of the wallet which should receive buyToken.
    slippagePercentage: float (default 0.01), # The total slippage to allow in this order. 0.01 = 1%.
}
```

Order Kind - Set to 'buy' to buy the exact amount of your `buyToken` and sell as little as possible to get that. Set to 'sell' to sell the exact amount of your `sellToken` and buy as much as you can with that.

### Return Values

**/sor Endpoint**

The `/sor` endpoint returns [SerializedSwapInfo](https://github.com/Sobal/balancer-api/blob/master/src/modules/sor/types.ts) which contains all the swaps and order information, but you must assemble the transaction to make this swap yourself.

**/order Endpoint**

The `/order` endpoint returns a [SorOrderResponse](https://github.com/Sobal/balancer-api/blob/master/src/modules/sor/types.ts) which contains transaction data that you can immediately post to chain.

Sometimes the returned order needs to be sent to the Batch Relayer (the `to` address will be the batch relayer). When this happens you must first approve the relayer with the vault so that it can make swaps on your behalf. You can do this by calling `setRelayerApproval(walletAddress, relayerAddress, true)` on the [vault](broken-reference), see an example in the [E2E Test Helpers](https://github.com/Sobal/balancer-api/blob/master/tests/lib/helpers.ts) file.

### Smart Order Router Examples

Below are some examples which you can use to build your own test data

**Swap USDC for wNEON on Neon**

```
curl -X POST -H "Content-Type: application/json" -d '{"sellToken":"0xEA6B04272f9f62F997F666F07D3a974134f7FFb9","buyToken":"0x202C35e517Fa803B537565c40F0a6965D7204609","orderKind":"sell", "amount":"100000", "gasPrice":"10000000"}' https://api.sobal.fi/sor/245022934
```

**Swap wSOL for an exact amount of wNEON**

```
curl -X POST -H "Content-Type: application/json" -d '{"sellToken":"0x5f38248f339Bf4e84A2caf4e4c0552862dC9F82a","buyToken":"0x202C35e517Fa803B537565c40F0a6965D7204609","orderKind":"buy", "amount":"1000000000000000000", "gasPrice":"10000000"}' https://api.sobal.fi/sor/245022934
```

###

\
\
