# LineItemPaymentTerm

Payment term for fee items. Null for metered/manual lines

## Example Usage

```python
from paygentic_sdk.models import LineItemPaymentTerm

# Open enum: unrecognized values are captured as UnrecognizedStr
value: LineItemPaymentTerm = "in_advance"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"in_advance"`
- `"in_arrears"`
