<!-- End user’s guide > Wrangler user guide > Transformation steps > Math steps > Sequence -->

##### Sequence

The **Sequence** step generates an arithmetic sequence of integer numbers. You can use it to add row numbers or create an artificial key.

###### Parameters

- **Sequence start**: required, the initial value of the sequence. The first generated value equals this start value. Can be a negative number. Default is `1`.
- **Sequence step**: required, the increment between consecutive values. The sequence increases by this value each step. Can be a negative number. Default is `1`.
- **Target column**: required, configure the column which will receive the output. Output will always be of integer type.
  - **Write result to the current column**: overwrite an existing column with the sequence values.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically.

###### Examples
Simple row numbering
To number rows in a data set starting from 1, use the default settings with **Sequence start** = `1` and **Sequence step** = `1`:

| Row | Sequence value |
| --- | --- |
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |
Starting from a specific value
To generate sequence starting from 100 with step 10, set **Sequence start** = `100` and **Sequence step** = `10`:

| Row | Sequence value |
| --- | --- |
| 1 | 100 |
| 2 | 110 |
| 3 | 120 |
| 4 | 130 |
Descending sequence
To generate a descending sequence, use a negative step. For example, **Sequence start** = `10` and **Sequence step** = `-1`:

| Row | Sequence value |
| --- | --- |
| 1 | 10 |
| 2 | 9 |
| 3 | 8 |
| 4 | 7 |

###### Remarks

- The sequence is always of integer type, regardless of the target column type.
- If overwriting an existing column, that column will be converted to integer type.
- The sequence values are consecutive according to the specified start and step, regardless of the actual data values in other columns.
