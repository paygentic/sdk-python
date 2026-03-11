# PaymentStatus

Current status of the payment.

## Example Usage

```python
from paygentic_sdk.models import PaymentStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: PaymentStatus = "pending"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"pending"`
- `"processing"`
- `"completed"`
- `"expired"`
- `"cancelled"`
