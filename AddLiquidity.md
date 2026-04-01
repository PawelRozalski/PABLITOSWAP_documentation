## ADD LIQUIDITY

## Goal:
User provides token A and B and receives LP tokens (shares token) representing their share of the pool


## First liquidity provider:

If the pool is empty
Formula:
liquidity = sqrt(amountA * amountB)

Why:
- sets initial price ratio
- defines base liquidity


## Next liquidity providers:

User must deposit tokens in the same ratio as the pool
Formula:
amountA / reserveA == amountB / reserveB

Liquidity is calculated as:
liquidityA = (amountA * totalLiquidity) / reserveA  
liquidityB = (amountB * totalLiquidity) / reserveB  

liquidity = min(liquidityA, liquidityB)

Why:
- preserves price
- prevents imbalance


## State updates

- userLiquidity increases
- totalLiquidity increases
- reserves increase


## Edge cases

- wrong ratio = revert
- liquidity == 0 ,revert
