# PermitDetailStatus

One of FILED, ISSUED, IN_PROGRESS, FINAL, EXPIRED, CANCELLED, REVOKED, INTERCONNECTED, UNKNOWN -- normalised by us from each source's own vocabulary. UNKNOWN means the source published no status, never that the permit is inactive. INTERCONNECTED comes from the California NEM solar feed.

## Example Usage

```python
from permitstack.models import PermitDetailStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: PermitDetailStatus = "FILED"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"FILED"`
- `"ISSUED"`
- `"IN_PROGRESS"`
- `"FINAL"`
- `"EXPIRED"`
- `"CANCELLED"`
- `"REVOKED"`
- `"UNKNOWN"`
- `"INTERCONNECTED"`
