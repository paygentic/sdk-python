# DisputeWithCustomerStatus

Current status of the dispute

## Example Usage

```python
from paygentic_sdk.models import DisputeWithCustomerStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: DisputeWithCustomerStatus = "pending"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"pending"`
- `"accepted"`
- `"declined"`
