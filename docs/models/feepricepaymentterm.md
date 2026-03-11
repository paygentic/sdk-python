# FeePricePaymentTerm

When the fee is charged relative to the billing period.

## Example Usage

```python
from paygentic_sdk.models import FeePricePaymentTerm

# Open enum: unrecognized values are captured as UnrecognizedStr
value: FeePricePaymentTerm = "in_advance"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"in_advance"`
- `"in_arrears"`
