# BatteryRetrofitCandidatesRequest


## Fields

| Field                                  | Type                                   | Required                               | Description                            |
| -------------------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- |
| `state`                                | *OptionalNullable[str]*                | :heavy_minus_sign:                     | 2-letter state code                    |
| `city`                                 | *OptionalNullable[str]*                | :heavy_minus_sign:                     | City name                              |
| `zip_code`                             | *OptionalNullable[str]*                | :heavy_minus_sign:                     | 5-digit ZIP                            |
| `jurisdiction`                         | *OptionalNullable[str]*                | :heavy_minus_sign:                     | Jurisdiction name (partial)            |
| `min_age_years`                        | *Optional[float]*                      | :heavy_minus_sign:                     | Minimum age of the PV permit, in years |
| `max_age_years`                        | *Optional[float]*                      | :heavy_minus_sign:                     | Maximum age of the PV permit, in years |
| `page`                                 | *Optional[int]*                        | :heavy_minus_sign:                     | N/A                                    |
| `per_page`                             | *Optional[int]*                        | :heavy_minus_sign:                     | N/A                                    |