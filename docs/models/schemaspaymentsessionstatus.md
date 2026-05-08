# SchemasPaymentSessionStatus

Lifecycle status of the session.

## Example Usage

```python
from paygentic_sdk.models import SchemasPaymentSessionStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: SchemasPaymentSessionStatus = "pending"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"pending"`
- `"processing"`
- `"completed"`
- `"failed"`
- `"expired"`
- `"cancelled"`
