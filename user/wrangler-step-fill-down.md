<!-- End user’s guide > Wrangler user guide > Transformation steps > Error handling steps > Fill down -->

##### Fill down

The **Fill down** step replaces [empty values](wrangler-faq.md#how-do-i-work-with-empty-values-whats-the-difference-between-null-and-empty) in a column with the last preceding available non-empty value from the same column. This helps maintain consistency in datasets by ensuring that gaps in data are filled with relevant preceding values, making it useful for structured and sequential data processing.

###### Parameters

- **Input column**: required, select the column where the step will be applied to replace empty values.

###### Example

Imagine you have a sales report that includes the Region for each sale, but only the first sale in each region is labeled, and the following rows are left empty. To organize the data better, you want to fill down the region name for all sales in the same region.

| Region | Sales | Region | Sales |
| --- | --- | --- | --- |
| Before the *Fill down* step is applied |  | After the *Fill down* step is applied |  |
| North | 1000 | North | 1000 |
| *No value* | 1500 | North | 1500 |
| *No value* | 2000 | North | 2000 |
| South | 1200 | South | 1200 |
| *No value* | 1300 | South | 1300 |
| East | 1700 | East | 1700 |
| *No value* | 1800 | East | 1800 |

###### See also

- [Error handling in Wrangler](transforming-data.md#error-handling-in-wrangler)
- [Remove rows with errors step](wrangler-step-remove-rows-with-errors.md)
- [Replace errors step](wrangler-step-replace-errors.md)
- [Replace empty values step](wrangler-step-replace-empty.md)
- [Clear error cells step](wrangler-step-clear-error-cells.md)
