## REMOVE LIQUIDITY

## Goal:
User burns share tokens to receive token A and token B proportionally to their share


## Calculate how many A and B tokens, to get based on share tokens:

Formula:

amountA = (liquidity * reserveA) / totalLiquidity
amountB = (liquidity * reserveB) / totalLiquidity


Why:

Share tokens represent the user proportional ownership of the entire pool

When a user burns share tokens, they withdraw the same percentage of both reserves (token A and token B)

The formulas ensure that:
- the user receives tokens in the correct proportion
- the pool ratio (the price) is not changed
- fairness is maintained between all liquidity providers

Example:
If a user owns 2% of totalLiquidity, they receive 2% of reserveA and 2% of reserveB.


## State updates

- userLiquidity decreased
- totalLiquidity decreased
- reserves decreased


## Edge cases

- liquidity must be greater than 0
- pool must have liquidity
- user can not burn more share tokens than they own


## Security

State is updated before token transfers to prevent reentrancy attacks


## Notes

Removing liquidity does not change the price, as tokens are withdrawn proportionally
