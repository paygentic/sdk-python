# SubscriptionProposalStatus

`pending` until a person approves or rejects the proposal.

## Example Usage

```python
from paygentic_sdk.models import SubscriptionProposalStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: SubscriptionProposalStatus = "pending"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"pending"`
- `"approved"`
- `"rejected"`
