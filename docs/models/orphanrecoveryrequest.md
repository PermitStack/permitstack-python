# OrphanRecoveryRequest


## Fields

| Field                                                | Type                                                 | Required                                             | Description                                          |
| ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- |
| `installer`                                          | *str*                                                | :heavy_check_mark:                                   | Installer name to match (contractor/applicant/owner) |
| `state`                                              | *OptionalNullable[str]*                              | :heavy_minus_sign:                                   | 2-letter state code                                  |
| `city`                                               | *OptionalNullable[str]*                              | :heavy_minus_sign:                                   | City name                                            |
| `zip_code`                                           | *OptionalNullable[str]*                              | :heavy_minus_sign:                                   | 5-digit ZIP                                          |
| `jurisdiction`                                       | *OptionalNullable[str]*                              | :heavy_minus_sign:                                   | Jurisdiction name (partial)                          |
| `page`                                               | *Optional[int]*                                      | :heavy_minus_sign:                                   | N/A                                                  |
| `per_page`                                           | *Optional[int]*                                      | :heavy_minus_sign:                                   | N/A                                                  |