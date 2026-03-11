# CreatePricePaymentTerm

Billing timing preference. For billable metrics: 'instant' (charges immediately) or 'in_arrears' (charges at period end). For fees: 'in_advance' (charges upfront) or 'in_arrears' (charges at period end).

## Example Usage

```python
from paygentic_sdk.models import CreatePricePaymentTerm
value: CreatePricePaymentTerm = "instant"
```


## Values

- `"instant"`
- `"in_arrears"`
- `"in_advance"`
