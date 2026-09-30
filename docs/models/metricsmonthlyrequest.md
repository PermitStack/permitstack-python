# MetricsMonthlyRequest


## Fields

| Field                              | Type                               | Required                           | Description                        |
| ---------------------------------- | ---------------------------------- | ---------------------------------- | ---------------------------------- |
| `state`                            | *OptionalNullable[str]*            | :heavy_minus_sign:                 | Two-letter state code, e.g. FL     |
| `city`                             | *OptionalNullable[str]*            | :heavy_minus_sign:                 | City name; case-insensitive        |
| `category`                         | *OptionalNullable[str]*            | :heavy_minus_sign:                 | Permit category, e.g. ROOFING      |
| `months`                           | *Optional[int]*                    | :heavy_minus_sign:                 | How many trailing months to return |