# LineItemStatus

Whether this item is pending or already on an invoice

## Example Usage

```python
from paygentic_sdk.models import LineItemStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: LineItemStatus = "pending"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"pending"`
- `"invoiced"`
