# ChangeReason

Why a change was made. `correction` repairs data that was entered wrong; `migration` moves a contract from another system; `commercial` is a real change to the deal; `contractual` applies a step the original contract scheduled, such as an annual uplift. Defaults to `unspecified`.

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
- `"contractual"`
