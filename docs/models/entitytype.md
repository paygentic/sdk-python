# EntityType

The type of Paygentic entity this external reference points at. `subscriptionProposal` and `subscription` references link a subscription proposal, and the subscription its approval creates, to the CRM record they come from. A `contract` reference links a contract to the CRM record it was created from. These three are read-only through these endpoints.

## Example Usage

```python
from paygentic_sdk.models import EntityType

# Open enum: unrecognized values are captured as UnrecognizedStr
value: EntityType = "item"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"item"`
- `"customer"`
- `"subscriptionProposal"`
- `"subscription"`
- `"contract"`
