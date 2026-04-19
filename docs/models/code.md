# Code

Optional semantic business error code for machine-readable discrimination (e.g. 'TAX_NOT_ENABLED'). UPPER_SNAKE_CASE. Clients should check this field, not message.

## Example Usage

```python
from paygentic_sdk.models import Code

# Open enum: unrecognized values are captured as UnrecognizedStr
value: Code = "TAX_NOT_ENABLED"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"TAX_NOT_ENABLED"`
- `"PAYMENT_SESSION_EXPIRED"`
