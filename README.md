# PABLITOSWAP DEX

PABLITOSWAP is Automated Market Maker (AMM) decentralized exchange


The protocol allows users to:

- swap between two ERC20 tokens
- provide liquidity to earn fees
- remove liquidity proportionally to their share


The system is based on the constant product formula:

x * y = k


## Contracts Architecture:

Contracts:

1. Main PablitoSwap.sol contract:

- entry point (user interaction layer)
- forwards calls to LP contract

2. Core logic PablitoSwapLP.sol contract:

- core AMM logic
- manages reserves
- executes swaps
- handles liquidity



Protocol flow PablitoSwapLP contract:

> Add Liquidity

User > addLiquidity()

- tokens transferred to contract
- LP share recorded
- reserves updated


> Remove Liquidity

User > removeLiquidity()

- LP tokens burned
- proportional tokens returned
- reserves updated


> Calculate amount out – view function used for estimate swap results (frontend / bots)


> Swap

User > swap(tokenIn, amountIn)

- amountOut calculated (AMM formula)
- tokens transferred
- reserves updated


Work:
- price is determined by pool reserves
- trades follow AMM (x * y = k)
- fee is applied on input amount
- fees stay in the pool and reward LPs

