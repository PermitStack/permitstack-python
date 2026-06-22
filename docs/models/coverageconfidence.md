# CoverageConfidence

Honest read on whether a `found: false` is meaningful or just missing data.

The wedge competitors won't ship: a 'no permit on record' is only useful if we
actually cover that jurisdiction. We say so explicitly so an automated (e.g.
underwriting) workflow can tell UNKNOWN apart from genuinely-no-work.


## Fields

| Field                       | Type                        | Required                    | Description                 |
| --------------------------- | --------------------------- | --------------------------- | --------------------------- |
| `confidence`                | *str*                       | :heavy_check_mark:          | N/A                         |
| `covered`                   | *bool*                      | :heavy_check_mark:          | N/A                         |
| `jurisdiction`              | *OptionalNullable[str]*     | :heavy_minus_sign:          | N/A                         |
| `data_status`               | *OptionalNullable[str]*     | :heavy_minus_sign:          | N/A                         |
| `jurisdiction_permit_count` | *OptionalNullable[int]*     | :heavy_minus_sign:          | N/A                         |
| `note`                      | *str*                       | :heavy_check_mark:          | N/A                         |