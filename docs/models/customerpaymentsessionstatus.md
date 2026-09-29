# CustomerPaymentSessionStatus

## Example Usage

```python
from paygentic_sdk.models import CustomerPaymentSessionStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: CustomerPaymentSessionStatus = "pending"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"pending"`
- `"processing"`
- `"completed"`
- `"failed"`
- `"expired"`
- `"cancelled"`
