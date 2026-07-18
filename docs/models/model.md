# Model

## Example Usage

```python
from paygentic_sdk.models import Model

# Open enum: unrecognized values are captured as UnrecognizedStr
value: Model = "standard"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"standard"`
- `"dynamic"`
- `"volume"`
- `"percentage"`
