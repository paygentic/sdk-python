# ApprovalDecision

## Example Usage

```python
from paygentic_sdk.models import ApprovalDecision

# Open enum: unrecognized values are captured as UnrecognizedStr
value: ApprovalDecision = "pending"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"pending"`
- `"approved"`
- `"rejected"`
- `"cancelled"`
