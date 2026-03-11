# DisputeStatus

Current status of the dispute

## Example Usage

```python
from paygentic_sdk.models import DisputeStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: DisputeStatus = "pending"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"pending"`
- `"accepted"`
- `"declined"`
