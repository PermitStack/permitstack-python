# PermitEnrichment

Curated subset of the offline LLM enrichment (permits.enriched_data).

Present only on the ~1-2% of permits that have been enriched so far
(prioritized toward SOLAR/ROOFING/NEW_CONSTRUCTION). null otherwise.


## Fields

| Field                     | Type                      | Required                  | Description               |
| ------------------------- | ------------------------- | ------------------------- | ------------------------- |
| `scope`                   | *OptionalNullable[str]*   | :heavy_minus_sign:        | N/A                       |
| `work_summary`            | *OptionalNullable[str]*   | :heavy_minus_sign:        | N/A                       |
| `solar_kw`                | *OptionalNullable[float]* | :heavy_minus_sign:        | N/A                       |
| `sqft`                    | *OptionalNullable[float]* | :heavy_minus_sign:        | N/A                       |
| `units`                   | *OptionalNullable[int]*   | :heavy_minus_sign:        | N/A                       |
| `is_residential`          | *OptionalNullable[bool]*  | :heavy_minus_sign:        | N/A                       |
| `is_commercial`           | *OptionalNullable[bool]*  | :heavy_minus_sign:        | N/A                       |
| `materials`               | List[*str*]               | :heavy_minus_sign:        | N/A                       |