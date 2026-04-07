<!-- End user’s guide > Wrangler user guide > Transformation steps > Date manipulation steps > Current date and time -->

##### Current date and time

The **Current date and time** step writes current date and time into designated column. Same value will be written into each row in dataset.

###### Parameters

- **Target column**: required, configure the column which will receive the current date and time. Output will always be of date type.
  - **Overwrite existing column**: overwrite existing column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed at the very end of the dataset.

###### Examples

| Output value | Description |
| --- | --- |
| 2023-03-06 12:34:16.285 | Current date and time |

###### Remarks

- The step will return the same value for each row in the data set regardless of how long the job execution takes. The value written is the date and time when the Wrangler job was started.
- The value returned is with millisecond precision.

###### See also

- [Date add/subtract](wrangler-step-date-add-subtract.md)
- [Date difference](wrangler-step-date-diff.md)
- [Get part of date](wrangler-step-get-date.md)
- [`today`](../developer/date-functions-ctl2.md#today) function in CTL.
