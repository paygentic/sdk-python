# EventType

Type of event: 'usage' for billable metric events, 'fee' for fee events

## Example Usage

```python
from paygentic_sdk.models import EventType

# Open enum: unrecognized values are captured as UnrecognizedStr
value: EventType = "usage"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"usage"`
- `"fee"`
