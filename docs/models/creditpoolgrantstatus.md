# CreditPoolGrantStatus

Where the grant stands now. `active` grants have started and are neither expired nor voided; a fully used grant stays `active` with a `remainingBalance` of 0. `scheduled` grants start later. `expired` grants passed their expiry. `voided` grants were cancelled.

## Example Usage

```python
from paygentic_sdk.models import CreditPoolGrantStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: CreditPoolGrantStatus = "active"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"active"`
- `"scheduled"`
- `"expired"`
- `"voided"`
