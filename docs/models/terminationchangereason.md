# TerminationChangeReason

Why the subscription was terminated. Null while it is not terminated.

## Example Usage

```python
from paygentic_sdk.models import TerminationChangeReason

# Open enum: unrecognized values are captured as UnrecognizedStr
value: TerminationChangeReason = "commercial"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"commercial"`
- `"correction"`
- `"migration"`
- `"unspecified"`
