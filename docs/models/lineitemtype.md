# LineItemType

Type of line item: 'charge' for regular billing, 'refund' for refunded items (amounts are negated)

## Example Usage

```python
from paygentic_sdk.models import LineItemType

# Open enum: unrecognized values are captured as UnrecognizedStr
value: LineItemType = "charge"
```


## Values

| Name     | Value    |
| -------- | -------- |
| `CHARGE` | charge   |
| `REFUND` | refund   |