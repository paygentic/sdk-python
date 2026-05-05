# PaymentSessionStatus

Lifecycle status of the session.

## Example Usage

```python
from paygentic_sdk.models import PaymentSessionStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: PaymentSessionStatus = "pending"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"pending"`
- `"processing"`
- `"completed"`
- `"failed"`
- `"expired"`
- `"cancelled"`
