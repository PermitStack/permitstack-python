# JurisdictionCoverage

How current one jurisdiction's data is, for the jurisdictions on THIS page of results.

Lets you tell "this source has not yet published the window you asked about" apart from
"this data is missing": `data_through` is the newest permit we hold for the jurisdiction,
and `with_contractor` shows how many rows on this page carry a contractor name.


## Fields

| Field                   | Type                    | Required                | Description             |
| ----------------------- | ----------------------- | ----------------------- | ----------------------- |
| `jurisdiction`          | *str*                   | :heavy_check_mark:      | N/A                     |
| `data_through`          | *OptionalNullable[str]* | :heavy_minus_sign:      | N/A                     |
| `status`                | *Optional[str]*         | :heavy_minus_sign:      | N/A                     |
| `results_on_page`       | *Optional[int]*         | :heavy_minus_sign:      | N/A                     |
| `with_contractor`       | *Optional[int]*         | :heavy_minus_sign:      | N/A                     |