# Blocks Subgraph

In order for our dApp and SDK to accurately build data, we utilise a block indexing subgraph which stores data for every block on chain

These subgraphs may be either self deployed and maintained, or we may utilise an already deployed subgraph from a reputable source.

We welcome public utilisation of our Subgraphs, and are open to further develop such as adding features where a request is made via our GitHub repository.

Source code: [https://github.com/Sobal/network-blocks](https://github.com/Sobal/network-blocks)

### Subgraphs Listing

| Network                      | Subgraph URL                                                                                                                                                 | Start Block # | Maintainer |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------- | ---------- |
| <p>Neon</p><p>#245022934</p> | [https://neon-subgraph.sobal.fi/sobal-neon-blocks](https://neon-subgraph.sobal.fi/sobal-neon-blocks)                                                         | 218300000     | Sobal      |
| <p>Base</p><p>#8453</p>      | [https://api.studio.thegraph.com/query/50526/sobal-base-blocks/version/latest](https://api.studio.thegraph.com/query/50526/sobal-base-blocks/version/latest) | 0             | Sobal      |

### Example Queries

Get comprehensive data on the latest blocks indexed

```
{
  blocks(orderDirection: desc, orderBy: number) {
    id
    number
    difficulty
    gasLimit
    gasUsed
    parentHash
    receiptsRoot
    size
    stateRoot
    timestamp
    totalDifficulty
    transactionsRoot
    unclesHash
  }
}
```

Query data from a specific block, in this example block number `209880000`

```
{
  block(id: "0xcb259d795bf2a2b9f989c93dd5bf07c9a17c265baed269512955db3bc980bf3d") {
    author
    difficulty
    gasLimit
    gasUsed
    number
    parentHash
    receiptsRoot
    size
    stateRoot
    timestamp
    unclesHash
    transactionsRoot
    totalDifficulty
  }
}
```
