# PriceRateType

What properties.unitPrice is denominated in. 'amount' (the default) is an amount of the invoice currency for each unit metered, so the quantity is the multiplier. 'proportion' is the reverse: a dimensionless share of a currency-denominated quantity, so '0.02' is 2% and the invoice prints '2.00%'. Presentation only. Requires a standard metered price in real currency.

## Example Usage

```python
from paygentic_sdk.models import PriceRateType

# Open enum: unrecognized values are captured as UnrecognizedStr
value: PriceRateType = "amount"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"amount"`
- `"proportion"`
