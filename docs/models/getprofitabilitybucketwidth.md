# GetProfitabilityBucketWidth

Time bucket granularity for the per-customer revenue trend. When omitted, the server picks a reasonable bucket from the window length.

## Example Usage

```python
from paygentic_sdk.models import GetProfitabilityBucketWidth
value: GetProfitabilityBucketWidth = "hour"
```


## Values

- `"hour"`
- `"day"`
- `"week"`
