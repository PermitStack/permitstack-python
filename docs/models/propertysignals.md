# PropertySignals

Boolean/scalar rollups useful for underwriting, valuation and diligence.

Derived from permit category + tags + offline enrichment across every
permit matched at the address. Dates are the most-recent permit of that
kind (ISO yyyy-mm-dd) so you can reason about roof/solar/pool age.


## Fields

| Field                     | Type                      | Required                  | Description               |
| ------------------------- | ------------------------- | ------------------------- | ------------------------- |
| `has_solar`               | *Optional[bool]*          | :heavy_minus_sign:        | N/A                       |
| `solar_kw`                | *OptionalNullable[float]* | :heavy_minus_sign:        | N/A                       |
| `last_solar_date`         | *OptionalNullable[str]*   | :heavy_minus_sign:        | N/A                       |
| `has_battery`             | *Optional[bool]*          | :heavy_minus_sign:        | N/A                       |
| `last_battery_date`       | *OptionalNullable[str]*   | :heavy_minus_sign:        | N/A                       |
| `has_roofing`             | *Optional[bool]*          | :heavy_minus_sign:        | N/A                       |
| `last_roofing_date`       | *OptionalNullable[str]*   | :heavy_minus_sign:        | N/A                       |
| `has_pool`                | *Optional[bool]*          | :heavy_minus_sign:        | N/A                       |
| `last_pool_date`          | *OptionalNullable[str]*   | :heavy_minus_sign:        | N/A                       |
| `has_addition`            | *Optional[bool]*          | :heavy_minus_sign:        | N/A                       |
| `has_new_construction`    | *Optional[bool]*          | :heavy_minus_sign:        | N/A                       |
| `has_electrical`          | *Optional[bool]*          | :heavy_minus_sign:        | N/A                       |
| `has_hvac`                | *Optional[bool]*          | :heavy_minus_sign:        | N/A                       |
| `last_hvac_date`          | *OptionalNullable[str]*   | :heavy_minus_sign:        | N/A                       |
| `has_plumbing`            | *Optional[bool]*          | :heavy_minus_sign:        | N/A                       |
| `has_demolition`          | *Optional[bool]*          | :heavy_minus_sign:        | N/A                       |
| `last_activity_date`      | *OptionalNullable[str]*   | :heavy_minus_sign:        | N/A                       |