# Reason

Coded failure reason. `grant_mint_failed` means the entitlement was created but its initial metered grant could not be minted; re-running this reconciliation retries the mint.

## Example Usage

```python
from paygentic_sdk.models import Reason

# Open enum: unrecognized values are captured as UnrecognizedStr
value: Reason = "entitlement_failed"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"entitlement_failed"`
- `"grant_mint_failed"`
