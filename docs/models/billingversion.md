# BillingVersion

Billing engine version. Only 1 (Standard, line-item billing with metered usage support) is accepted for new plans; omitting the field defaults to 1. 0 (Legacy, fee-schedule billing) is rejected — it exists only on plans created before this restriction.

## Example Usage

```python
from paygentic_sdk.models import BillingVersion
value: BillingVersion = 0
```


## Values

- `0`
- `1`
