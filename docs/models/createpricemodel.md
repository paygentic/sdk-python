# CreatePriceModel

Pricing calculation model. Required for billable metrics, optional for fees (defaults to 'standard').

## Example Usage

```python
from paygentic_sdk.models import CreatePriceModel
value: CreatePriceModel = "standard"
```


## Values

| Name         | Value        |
| ------------ | ------------ |
| `STANDARD`   | standard     |
| `DYNAMIC`    | dynamic      |
| `VOLUME`     | volume       |
| `PERCENTAGE` | percentage   |