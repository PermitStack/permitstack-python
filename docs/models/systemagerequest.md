# SystemAgeRequest


## Fields

| Field                                      | Type                                       | Required                                   | Description                                |
| ------------------------------------------ | ------------------------------------------ | ------------------------------------------ | ------------------------------------------ |
| `trade`                                    | *str*                                      | :heavy_check_mark:                         | roofing \| hvac \| mechanical \| solar \| pool |
| `state`                                    | *OptionalNullable[str]*                    | :heavy_minus_sign:                         | 2-letter state code                        |
| `city`                                     | *OptionalNullable[str]*                    | :heavy_minus_sign:                         | City name                                  |
| `zip_code`                                 | *OptionalNullable[str]*                    | :heavy_minus_sign:                         | 5-digit ZIP                                |
| `jurisdiction`                             | *OptionalNullable[str]*                    | :heavy_minus_sign:                         | Jurisdiction name (partial)                |
| `min_age_years`                            | *OptionalNullable[float]*                  | :heavy_minus_sign:                         | Override the trade's default minimum age   |
| `max_age_years`                            | *OptionalNullable[float]*                  | :heavy_minus_sign:                         | Override the trade's default maximum age   |
| `page`                                     | *Optional[int]*                            | :heavy_minus_sign:                         | N/A                                        |
| `per_page`                                 | *Optional[int]*                            | :heavy_minus_sign:                         | N/A                                        |