# EntitlementStatus

Current status of the entitlement.

## Example Usage

```python
from paygentic_sdk.models import EntitlementStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: EntitlementStatus = "active"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"active"`
- `"canceled"`
- `"expired"`
