# GetPropertyHistoryRequest


## Fields

| Field                                                    | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `address`                                                | *str*                                                    | :heavy_check_mark:                                       | Street address to look up (e.g. '123 Main St')           |
| `city`                                                   | *OptionalNullable[str]*                                  | :heavy_minus_sign:                                       | Optional city to disambiguate identical street addresses |
| `state`                                                  | *OptionalNullable[str]*                                  | :heavy_minus_sign:                                       | Optional 2-letter state code                             |
| `zip`                                                    | *OptionalNullable[str]*                                  | :heavy_minus_sign:                                       | Optional ZIP (prefix-matched)                            |
| `page`                                                   | *Optional[int]*                                          | :heavy_minus_sign:                                       | N/A                                                      |
| `per_page`                                               | *Optional[int]*                                          | :heavy_minus_sign:                                       | N/A                                                      |