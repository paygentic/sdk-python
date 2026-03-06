# PaymentStatus

Current status of the payment.

## Example Usage

```python
from paygentic_sdk.models import PaymentStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: PaymentStatus = "pending"
```


## Values

| Name         | Value        |
| ------------ | ------------ |
| `PENDING`    | pending      |
| `PROCESSING` | processing   |
| `COMPLETED`  | completed    |
| `EXPIRED`    | expired      |
| `CANCELLED`  | cancelled    |