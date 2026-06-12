# MerchantIntegrationStatus

Connection lifecycle state. Live Ampersand health is separate and not stored here.

## Example Usage

```python
from paygentic_sdk.models import MerchantIntegrationStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: MerchantIntegrationStatus = "active"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"active"`
- `"disconnected"`
- `"error"`
