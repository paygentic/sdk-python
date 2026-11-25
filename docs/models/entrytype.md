# EntryType

What kind of balance movement this entry represents.

## Example Usage

```python
from paygentic_sdk.models import EntryType

# Open enum: unrecognized values are captured as UnrecognizedStr
value: EntryType = "increment"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"increment"`
- `"decrement"`
- `"void"`
- `"expiration"`
