# SubscriptionProposalDecisionDecision

`approve` creates the subscription and makes the proposal `approved`. `reject` rejects the proposal. Either is final: the proposal never becomes `pending` again.

## Example Usage

```python
from paygentic_sdk.models import SubscriptionProposalDecisionDecision
value: SubscriptionProposalDecisionDecision = "approve"
```


## Values

- `"approve"`
- `"reject"`
