<!-- End user’s guide > Wrangler user guide > Transformation steps > Date manipulation steps > Date add/subtract -->

##### Date add/subtract

The **Date add/subtract** step adds or subtracts a specified number of time units *(days, weeks, months, years, hours, minutes, seconds, milliseconds)*.

###### Parameters

- **Input date**: required, choose whether to use today’s date or dates from a column.
  - **Today**: add or subtract time units from today’s date. This value changes daily.
  - **Columns group** columns: Pick an existing date column from the list.
- **Number of units**: required, the number of units to be added or subtracted from the selected date. Use negative values to subtract.
  - **Constant value**: enter a constant value.
  - **Select from column**: choose a column with integer values. The value from each row will be applied to today’s date or the corresponding row in the input column.
- **Unit**: required, the time unit to be added/subtracted. Pick one of the following:
  - days
  - weeks
  - months
  - years
  - hours
  - minutes
  - seconds
  - milliseconds
- **Target column**: required, configure the column which will receive the output.
  - **Overwrite existing column**: output data into an existing column.
  - **Create new column with name**: create a new column with the specified name. Name of the new column can contain spaces or special characters - the technical column name will be created automatically. The new column will be placed right **next to the selected Input date column**, if a column is selected. If **Today** is selected as the input date, the column will be **added at the end of the table.**

###### Examples

Sample date: `2023-01-09 03:11:00`

| Input date | Unit | Number of units | Result | Note |
| --- | --- | --- | --- | --- |
| `2023-01-09 03:11:00` | Days | 8 | 2023-01-17 03:11:00 |  |
| `2023-01-09 03:11:00` | Days | -8 | 2023-01-01 03:11:00 |  |
| `2023-01-09 03:11:00` | Months | 2 | 2023-03-09 03:11:00 |  |
| `2023-01-09 03:11:00` | Days | 60 | 2023-03-10 03:11:00 | Note the difference between adding 2 months vs. 60 days - the months add calendar months so add different number of days depending on the input date. |
| `2023-01-09 03:11:00` | Minutes | 123456 | `2023-08-02 21:02:00` | Any number works as number of units - there is no need to limit the values to small numbers. |
| *No value* | Any | Any | *Error* | Trying to add/subtract to/from empty values results in an error. |
| *Error* | Any | Any | *Error* | Applying the step to an *Error* value results in an *Error*. |

###### See also

- [Current date and time step](wrangler-step-current-datetime.md)
- [Date difference step](wrangler-step-date-diff.md)
- [Get part of date step](wrangler-step-get-date.md)
- [`dateAdd`](../developer/date-functions-ctl2.md#dateadd) function in CTL.
