<!-- End user’s guide > Wrangler user guide > Transformation steps > Date manipulation steps > Date difference -->

##### Date difference

The **Date difference** step calculates the time difference in the specified time unit (*days, weeks, months, years, hours, minutes, seconds, or milliseconds*) between two date columns.

###### Parameters

- **First date**: required, choose whether to use today’s date or dates from a column.
  - **Today**: add or subtract time units from today’s date. This value changes daily.
  - **Columns group** columns: Pick an existing date column from the list.
- **Second date**: required, select a date column from the column list.
  - **Today**: add or subtract time units from today’s date. This value changes daily.
  - **Columns group** columns: Pick an existing date column from the list.
- **Unit**: required, select the date unit that will be used in the calculation (*days, weeks, months, years, hours, minutes, seconds, milliseconds*).
- **Target column**: required, configure the column which will receive the output. Output will always be an integer.
  - **Overwrite existing column**: output data into an existing column.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be **added at the end of the table**.

###### Examples

| First date column | Second date column | Unit | Result | Notes |
| --- | --- | --- | --- | --- |
| 2023-03-31 | 2023-01-01 | Days | 89 |  |
| 2023-01-01 | 2023-03-31 | Days | -89 | Second date is after the first, result is negative. |
| 2023-03-31 | 2023-01-01 | Months | 2 |  |
| 2023-01-01 | 2023-03-31 | Months | -2 | Second date is after the first, result is negative. |
| 2023-03-25 04:51:25 | 2023-03-25 03:00:00 | Hours | 1 | Difference is 1 hour 51 minutes 25 seconds which is truncated to 1 hour. |
| 2023-03-25 04:51:25 | 2023-03-25 03:00:00 | Minutes | 111 | Difference is 1 hour 51 minutes 25 seconds which is 111 minutes and 25 seconds which is truncated to 111 minutes. |
| 2023-03-25 04:51:25 | 2023-03-25 03:00:00 | Seconds | 6685 | Difference is 6685 seconds exactly, no truncation is necessary. |
| *No value* | Any | Any | *Error* | *Error* |

###### Remarks

- The order of the dates in the step parameters matters. The step always calculates `First date` - `Second date`, which might result in negative values if `Second date` is after the `First date`.
- The result is truncated to the whole number of units. For example, if the time difference between the values is 2 hours 45 minutes, the result will be "2" if the time unit is *hours*.
- If any of the input dates is *No value*, the step will fail.
- If any of the input dates is an *Error*, the step will fail.

###### See also

- [Current date and time](wrangler-step-current-datetime.md)
- [Date add/subtract](wrangler-step-date-add-subtract.md)
- [Get part of date](wrangler-step-get-date.md)
- [`datediff`](../developer/date-functions-ctl2.md#datediff) function in CTL.
