# PermitSummaryCategory

Trade/work classification, UPPERCASE. One of: NEW_CONSTRUCTION, RENOVATION, DEMOLITION, ELECTRICAL, PLUMBING, MECHANICAL, ROOFING, SOLAR, BATTERY, EV_CHARGER, HVAC, FIRE_ALARM, SIGN, FENCE, POOL, FOUNDATION, ADDITION, INTERIOR_REMODEL, GRADING, OTHER. Derived by us from the permit type and description, not published by the city. NOTE when FILTERING: ?category=hvac matches HVAC *and* MECHANICAL, and ?category=mechanical does the same, because HVAC work is routinely filed as MECHANICAL -- they are one market and a bare equality would hide half of it.

## Example Usage

```python
from permitstack.models import PermitSummaryCategory

# Open enum: unrecognized values are captured as UnrecognizedStr
value: PermitSummaryCategory = "NEW_CONSTRUCTION"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"NEW_CONSTRUCTION"`
- `"RENOVATION"`
- `"DEMOLITION"`
- `"ELECTRICAL"`
- `"PLUMBING"`
- `"MECHANICAL"`
- `"ROOFING"`
- `"SOLAR"`
- `"BATTERY"`
- `"EV_CHARGER"`
- `"HVAC"`
- `"FIRE_ALARM"`
- `"SIGN"`
- `"FENCE"`
- `"POOL"`
- `"FOUNDATION"`
- `"ADDITION"`
- `"INTERIOR_REMODEL"`
- `"GRADING"`
- `"OTHER"`
