# Linear Math

## Overview

Linear math is designed to facilitate swaps between assets and their yield bearing, wrapped counterparts. For example, DAI and aDAI from Aave. This pairing is done using the identity function, with consideration for the exchange rate between the main (unwrapped) and wrapped assets. Linear pools are the base layer for boosted pools.

## Implementations

### TypeScript

Developers can use the TypeScript math implementations used by the Smart Order router

* [linearMath.ts](https://github.com/balancer/balancer-sor/blob/john/v2-package-linear/src/pools/linearPool/linearMath.ts)

## Invariant

The invariant of the linear math function is trivial in nature, similar to the constant sum invariant. The main difference being the exchange rate, or rate provider, being utilized for the wrapped tokens.

$$I = \sum_{t}({B_{t}*R_{t}})$$

Where

* $t$ ranges over the tokens in the pool
* $B\_t$ is the nominal balance of the token in the pool
* $R\_t$​ is the rate provider or exchange rate. For the main, unwrapped token R = 1

## Spot Price

Spot price is independent of the balances, and will depend on the exchange rates between the underlying assets only. This is defined as:

$$SP*{i}^{o} = {\frac{R*{i}}{R\_{o}}}$$

* $R\_i$ is the rate provider of token $i$ going into the pool
* $R\_o$ is the rate provider of token $o$ coming out of the pool

## Swap Equations

For linear pools, the unique factor of the swap equations is the swap fees. The fee structure incentivizes swappers to maintain the unwrapped balance of the tokens in the pool to remain between an upper ($T\_{2}$) and lower ($T\_{1}$) boundary. The swap equations can best be described by the following piece wise functions.

### outGivenIn

$$
A_{o} = \begin{cases} A_{i} * \frac{R_{i}}{R_{o}} & T_{1}\leq x\leq T_{2} \\ \\ A_{i} * \frac{R_{i}}{R_{o}} * (1 - \phi) & x\leq T_{1} \ or \ T_{2}\leq x \ \ \ When \ swap \ pushes \ pool \ out \ of \ bounds \\ \\ A_{i} * \frac{R_{i}}{R_{o}} * (1 + \phi) & x\leq T_{1} \ or \ T_{2}\leq x \ \ \ When \ swap \ pushes \ pool \ towards \ bounds\\ \end{cases}
$$

Where:

* $A\_{o}$ is the amount out. This represents the number of tokens a user will receive from a swap.
* $A\_{i}$ is the amount in. This represents the number of tokens a user will sell to perform a swap.
* $R\_{i}$ The rate provider value, or exchange rate of the token in.
* $R\_{o}$ The rate provider value, or exchange rate of the token out.
* $\phi$ - Represents the swap fee of the pool.
* $T\_{1}$ The lower target boundary of the unwrapped token balance
* $T\_{2}$ The upper target boundary of the unwrapped token balance
* $x$ is the unwrapped token balance within the pool.

### inGivenOut

$$
A_{i} = \begin{cases} A_{o} * \frac{R_{o}}{R_{i}} & T_{1}\leq x\leq T_{2} \\ \\ A_{o} * \frac{R_{o}}{R_{i}} * (1 - \phi) & x\leq T_{1} \ or \ T_{2}\leq x \ \ \ When \ swap \ pushes \ pool \ out \ of \ bounds \\ \\ A_{o} * \frac{R_{o}}{R_{i}} * (1 + \phi) & x\leq T_{1} \ or \ T_{2}\leq x \ \ \ When \ swap \ pushes \ pool \ towards \ bounds\\ \end{cases}
$$

Where:

* $A\_{i}$ is the amount in. This represents the number of tokens a user will sell to perform a swap.
* $R\_{i}$ The rate provider value, or exchange rate of the token in.
* $R\_{o}$ The rate provider value, or exchange rate of the token out.
* $\phi$ - Represents the swap fee of the pool.
* $T\_{1}$ The lower target boundary of the unwrapped token balance
* $T\_{2}$ The upper target boundary of the unwrapped token balance
* $x$ is the unwrapped token balance within the pool.
