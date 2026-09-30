# GetPermitsByAddressRequest


## Fields

| Field                                                 | Type                                                  | Required                                              | Description                                           |
| ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
| `address`                                             | *str*                                                 | :heavy_check_mark:                                    | N/A                                                   |
| `page`                                                | *Optional[int]*                                       | :heavy_minus_sign:                                    | N/A                                                   |
| `per_page`                                            | *Optional[int]*                                       | :heavy_minus_sign:                                    | N/A                                                   |
| `record_kind`                                         | *Optional[str]*                                       | :heavy_minus_sign:                                    | 'permit' (default), a specific record_kind, or 'all'. |