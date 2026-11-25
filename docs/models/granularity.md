# Granularity

Roll the ledger up into calendar-aligned buckets (UTC) instead of itemized entries. Calendar periods with no activity are omitted from the response. To see the individual entries behind a bucket, request the itemized ledger (omit `granularity`) with the same `entryType` filter and `from`/`to` narrowed to that bucket's `period`.

## Example Usage

```python
from paygentic_sdk.models import Granularity
value: Granularity = "hour"
```


## Values

- `"hour"`
- `"day"`
- `"month"`
