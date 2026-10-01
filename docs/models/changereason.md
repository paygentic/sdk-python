# ChangeReason

Why a change was made. `correction` fixes data to match what was agreed; `migration` moves a contract from another system; `commercial` is a real change to the deal. Defaults to `unspecified`.

## Example Usage

```python
from paygentic_sdk.models import ChangeReason

# Open enum: unrecognized values are captured as UnrecognizedStr
value: ChangeReason = "commercial"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"commercial"`
- `"correction"`
- `"migration"`
- `"unspecified"`
