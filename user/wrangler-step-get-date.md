<!-- End user’s guide > Wrangler user guide > Transformation steps > Date manipulation steps > Get part of date -->

##### Get part of date

The **Get part of date** step extracts the specified time unit *(day of week, day of month, month, year, hours, minutes, seconds, milliseconds)* from a date column.

###### Parameters

- **Input date**: required, choose whether to use today’s date or dates from a column.
  - **Today**: Use today’s date as the calculation basis. This value changes daily.
  - **Columns group** columns: Pick an existing date column from the list.
- **Part**: required, the time unit to be extracted from the input date. The following options are available:
  - day of week
  - day of month
  - month
  - year
  - hours
  - minutes
  - seconds
  - milliseconds
- **Target column**: required, configure the column which will receive the output. Output will always be an integer.
  - **Overwrite existing column**: overwrite existing column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right **next to the selected Input date column**, if a column is selected. If **Today** is selected as the input date, the column will be **added at the end of the table.**

###### Examples

Sample date: `2023-05-09 03:11:00`

| Date unit | Result |
| --- | --- |
| Day of week | 2 |
| Day of month | 9 |
| Month | 5 |
| Minute | 11 |

###### Returned values

The values returned by the step depend on the selected unit:

| Unit | Minimum value | Maximum value | Note |
| --- | --- | --- | --- |
| day of week | 1 | 7 (Sunday) | Value of 1 always means Monday and 7 is Sunday regardless of the start day of the week. |
| day of month | 1 | 31 |  |
| month | 1 | 12 |  |
| year | 292278994 (292 million) | -292278994 (-292 million) | Dates can store exact date and time millions of years in the past or in the future. |
| hours | 0 | 23 | 24-hour format is used regardless of the display format of the input date column (i.e. 4pm will return 16). |
| minutes | 0 | 59 |  |
| seconds | 0 | 59 |  |
| milliseconds | 0 | 999 |  |

###### See also

- [Current date and time step](wrangler-step-current-datetime.md)
- [Date add/subtract step](wrangler-step-date-add-subtract.md)
- [Date difference step](wrangler-step-date-diff.md)
- [`getYear`](../developer/date-functions-ctl2.md#getyear) function in CTL
- [`getMonth`](../developer/date-functions-ctl2.md#getmonth) function in CTL
- [`getDay`](../developer/date-functions-ctl2.md#getday) function in CTL
- [`getHour`](../developer/date-functions-ctl2.md#gethour) function in CTL
- [`getMinute`](../developer/date-functions-ctl2.md#getminute) function in CTL
- [`getSecond`](../developer/date-functions-ctl2.md#getsecond) function in CTL
- [`getMillisecond`](../developer/date-functions-ctl2.md#getmillisecond) function in CTL
