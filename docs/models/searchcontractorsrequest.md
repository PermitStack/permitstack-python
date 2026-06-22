# SearchContractorsRequest


## Fields

| Field                                                 | Type                                                  | Required                                              | Description                                           |
| ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
| `name`                                                | *OptionalNullable[str]*                               | :heavy_minus_sign:                                    | Contractor name (partial match)                       |
| `state`                                               | *OptionalNullable[str]*                               | :heavy_minus_sign:                                    | 2-letter state code                                   |
| `city`                                                | *OptionalNullable[str]*                               | :heavy_minus_sign:                                    | City name                                             |
| `specialty`                                           | *OptionalNullable[str]*                               | :heavy_minus_sign:                                    | Specialty tag (e.g. solar, roofing, hvac)             |
| `min_permits`                                         | *OptionalNullable[int]*                               | :heavy_minus_sign:                                    | Minimum total permits                                 |
| `min_score`                                           | *OptionalNullable[int]*                               | :heavy_minus_sign:                                    | Minimum contractor activity score (0-100)             |
| `sort`                                                | *Optional[str]*                                       | :heavy_minus_sign:                                    | Sort order: 'score' (default), 'permits', or 'recent' |
| `page`                                                | *Optional[int]*                                       | :heavy_minus_sign:                                    | N/A                                                   |
| `per_page`                                            | *Optional[int]*                                       | :heavy_minus_sign:                                    | N/A                                                   |