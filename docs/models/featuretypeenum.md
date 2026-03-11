# FeatureTypeEnum

The type of feature: `boolean` (on/off), `static` (with config), or `metered` (usage-based).

## Example Usage

```python
from paygentic_sdk.models import FeatureTypeEnum

# Open enum: unrecognized values are captured as UnrecognizedStr
value: FeatureTypeEnum = "boolean"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"boolean"`
- `"static"`
- `"metered"`
