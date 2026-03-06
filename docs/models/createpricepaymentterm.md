# CreatePricePaymentTerm

Billing timing preference. For billable metrics: 'instant' (charges immediately) or 'in_arrears' (charges at period end). For fees: 'in_advance' (charges upfront) or 'in_arrears' (charges at period end).

## Example Usage

```python
from paygentic_sdk.models import CreatePricePaymentTerm
value: CreatePricePaymentTerm = "instant"
```


## Values

| Name         | Value        |
| ------------ | ------------ |
| `INSTANT`    | instant      |
| `IN_ARREARS` | in_arrears   |
| `IN_ADVANCE` | in_advance   |