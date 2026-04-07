<!-- End user’s guide > Wrangler user guide > Transformation steps > Data anonymization steps > Add noise to date -->

##### Add noise to date

The **Add noise to date** step can be used to anonymize date values. This step produces a new date that is within the specified range around the original value. See more details in [How are the new values calculated](wrangler-step-add-noise-to-date.md#how-are-the-new-values-calculated).

###### Parameters

- **Input column**: required, select a *date* column.
- **Noise amount**: required, enter the amount and unit by which to change the new date that will be randomly created from the original value. See [below](wrangler-step-add-noise-to-date.md#how-are-the-new-values-calculated) for more details about how the new values are generated.
  - The default value *is 10 days*.
  - Time units can be: *days*, *weeks*, *months*, *years*, *hours*, *minutes*, *seconds*, or *milliseconds*.
- **Truncate to date**: selected by default. When selected, time units are disregarded and always output as `0:00:00` in the result values.
- **Target column**: required, configure the column which will receive the output.
  - **Write result to the current column**: outputs data into the **Input column**.
  - **Create new column with name**: create a new column with the specified name. Name of the new column can contain spaces or special characters - the technical column name will be created automatically. The new column will be placed right next to the **Input column**.

###### How are the new values calculated

The step performs an operation that can be imagined as randomly shifting the original value by an amount that is smaller than the provided maximum.

It works by calculating lower and upper bounds for the new value. These are both based on the **Noise amount** parameter:

- Lower bound is calculated as `$originalValue - noiseAmount`
- Upper bound is calculated as `$originalValue + noiseAmount`

The calculation properly accounts for complexities of date math - short/long months, DST "jumps", leap years, etc.

Once the lower and upper bound is computed, a new random date is picked in the interval between those two values. This effectively means that you get a new random date and time value that is never more than specified amount of time away from the original value.

###### Examples

The example date below is in the `yyyy-MM-dd` format.

| Original date | Noise amount | Truncate to date only | Calculated range | Result amount |
| --- | --- | --- | --- | --- |
| 2023-03-01 | 10 days | Any | ±10 days | The result date will be between `February 19th, 2023` and `March 11th, 2023`. |
| 2023-03-01 | 10 weeks | Any | ±10 weeks | The result date will be between `December 21st, 2022` and `May 10th, 2023`. |
| 2023-03-01 08:00:00 | 10 weeks | Yes (checked) | ±10 weeks | The result date will be between `December 21st, 2022, 0:00:00` and `May 10th, 2023, 0:00:00`. |
| 2023-03-01 08:00:00 | 10 weeks | No (unchecked) | ±10 weeks | The result date and time will be between `December 21st, 2022, 0:00:00` and `May 10th, 2023, 23:59:59`. |
| 2023-03-01 08:00:00 | 12 hours | Yes (checked) | ±12 hours | The result date and time will be between `February 28th, 2023, 0:00:00` and `March 1st, 2023, 0:00:00`. |
| 2023-03-01 08:00:00 | 12 hours | No (unchecked) | ±12 hours | The result date and time will be between `February 28th, 2023, 20:00:00` and `March 1st, 2023, 20:00:00`. |
| *No value* | 12 hours | Any | Not calculated | `No value` (the result is an empty value). |

###### Remarks

- The dates are randomized again with every job run - you will get new values every time.
- The step does not modify empty values - they will remain empty even after the step. If you wish to handle these in some other way, please see [Working with empty values](wrangler-faq.md#how-do-i-work-with-empty-values-whats-the-difference-between-null-and-empty) for more information.

###### See also

- [Add noise to number step](wrangler-step-add-noise-to-number.md)
- [Replace text step](wrangler-step-replace-text.md)
- [`addNoise`](../developer/mathematical-functions-ctl2.md#addnoise) function.
