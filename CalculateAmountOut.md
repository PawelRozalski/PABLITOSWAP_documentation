## CALCULATE AMOUNT OUT

## Goal:
Returns the estimated amount output tokens user would receive for a given input amount, without executing swap

## Description:
This is view function use to simulate swap based on the current pool reserves and fee
It does not modify the contract state

## The function:
- applies the swap fee (0.3%)
- determines input and output reserves based on the selected token
- calculates the output amount using the constant product formula (x * y = k)
  
Formula:

amountOut = (amountInWithFee * reserveOut) / (reserveIn + amountInWithFee)

Why:

The function allows:
- frontends to display estimated swap results
- bots and external systems to evaluate trades
- users to preview result before executing swap

## Notes:
- The result is only estimate and may differend slightly due to rounding or state changes between transactions
- No tokens are transferred
- No state variables are updated
