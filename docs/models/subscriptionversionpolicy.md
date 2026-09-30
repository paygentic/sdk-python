# SubscriptionVersionPolicy

How the subscription follows new versions of its plan. `floating` follows the plan's default version: when the default changes, the subscription bills from the new default from its next billing period. `pinned` keeps the plan version that the subscription holds. A subscription created without a value is `floating`. A change to this value does not change a billing period that has already started.

## Example Usage

```python
from paygentic_sdk.models import SubscriptionVersionPolicy

# Open enum: unrecognized values are captured as UnrecognizedStr
value: SubscriptionVersionPolicy = "floating"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"floating"`
- `"pinned"`
