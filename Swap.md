## SWAP

## Goal:

Swap allows user to exchange one token for another (token A > token B or token B > token A) based on the AMM model. The user provides tokenIn and receives tokenOut


## Function signature:

function swap(address tokenIn, uint256 amountIn, uint256 minAmountOut) external;

Parameters:

- tokenIn = address of the token the user wants to swap from (must be tokenA or tokenB)
- amountIn = amount input tokens provided by the user
- minAmountOut = minimum acceptable amount of output tokens (slippage protection)


## Generally calculation:

The swap uses the constant product AMM model:

x * y = k

- x and y are pool reserves
- k remains constant (ignoring fees)


## Calculation amountOut:

amountOut = (amountWithoutFee * reserveOut) / (reserveIn + amountWithoutFee);

Where:

- amountInWithFee = amountIn * (1000 - fee) / 1000
- reserveIn = reserve of input token
- reserveOut = reserve of output token

Why:

- Ensures price is determined by pool reserves
- Maintains constant product invariant (x * y = k)
- Applies trading fee directly to the pool
- Automatically adjusts price based in liquidity


## Security:

- slippage protection:
require(amountOut >= minAmountOut);

- Input validation:
amountIn > 0
tokenIn must be vaild (A or B)
reserves must be > 0

- Interactions pattern:
calculation > validation > state update > external calls


## State Updates:

Depending on swap direction:

tokenA > tokenB:
reserveA += amountIn
reserveB -= amountOut

tokenB > tokenA:
reserveB += amountIn
reserveA -= amountOut


## Fee mechanizm:

- Fee is applied to amountIn
- Fee remains in the pool
- LP providers earn from fees proportionally to their share tokens


## Edge Cases:

amountIn == 0 > revert

amountOut == 0 > revert

invalid tokenIn > revert

insufficient liquidity > revert

slippage exceeded > revert


## Notes:

- swap changes the pool ratio (affects price)
- larger trades cause higher slippage
- deeper liquidity reduces price impact
- function does not return value > result is see via event or balance change


## Summary:

- enables token swap
- maintains > AMM invariant
- distributes fees to > LP providers
- dynamically adjusts price based by liquidity
