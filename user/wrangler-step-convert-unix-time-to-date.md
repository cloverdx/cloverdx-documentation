<!-- End user’s guide > Wrangler user guide > Transformation steps > Data conversion steps > Convert Unix time to date -->

##### Convert Unix time to date

The **Convert Unix time to date** step allows you to convert from a numeric Unix timestamp value to a date type. Unix timestamp is specified as a number of milliseconds since January 1st, 1970 (also called Unix epoch). Positive numbers refer to date and time after the epoch while negative values refer to date and time before the epoch. For example, timestamp 1680620400000 refers to Tuesday, April 4th, 2023, 15:00 GMT.

###### Parameters

- **Input column**: required, an integer column containing timestamps to convert to date.
- **Target column**: required, configure the column which will receive the output. Output will always be a date column.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

Note the value in the Output column in the examples will depend on formatting selected for the target column. Examples use `yyyy-MM-dd HH:mm:ss.SSS` formatting to display full date and time including milliseconds and use UTC time zone.

| Input value | Output value | Description |
| --- | --- | --- |
| 0 | 1970-01-01 00:00:00.000 | Value of 0 corresponds to Unix epoch start - midnight of January 1st, 1970. |
| 1680620400000 | 2023-04-04 15:00:00.000 | Positive values represent date and time after the Epoch start. |
| -14182980000 | 1969-07-20 20:17:00.000 | Negative values result in date and time before Epoch start. |
| *No value* | *No value* |  |

###### Remarks

- This steps changes type of the column from integer to date. Different formatting options will be available for the column after the conversion.

###### See also

- [long2date CTL function](../developer/conversion-functions-ctl2.md#long2date)
