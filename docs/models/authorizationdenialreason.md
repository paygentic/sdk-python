# AuthorizationDenialReason

Present on a 403 from the authorization check. Says why access was refused: the caller has no role that grants the permission, the OAuth token lacks the scope, or the caller is not a member of the organization.

## Example Usage

```python
from paygentic_sdk.models import AuthorizationDenialReason

# Open enum: unrecognized values are captured as UnrecognizedStr
value: AuthorizationDenialReason = "no_permission"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"no_permission"`
- `"insufficient_scope"`
- `"not_member"`
