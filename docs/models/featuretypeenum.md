# FeatureTypeEnum

The type of feature: `boolean` (on/off), `static` (with config), or `metered` (usage-based).

## Example Usage

```python
from paygentic_sdk.models import FeatureTypeEnum

# Open enum: unrecognized values are captured as UnrecognizedStr
value: FeatureTypeEnum = "boolean"
```


## Values

| Name      | Value     |
| --------- | --------- |
| `BOOLEAN` | boolean   |
| `STATIC`  | static    |
| `METERED` | metered   |