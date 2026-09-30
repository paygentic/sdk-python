# SubscriptionIntervalKind

plan_line if the plan version has a line with this priceKey. subscription_owned if it does not, so the interval belongs to this subscription only. After an add, check the kind. A mistyped priceKey creates a subscription_owned interval.

## Example Usage

```python
from paygentic_sdk.models import SubscriptionIntervalKind

# Open enum: unrecognized values are captured as UnrecognizedStr
value: SubscriptionIntervalKind = "plan_line"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"plan_line"`
- `"subscription_owned"`
