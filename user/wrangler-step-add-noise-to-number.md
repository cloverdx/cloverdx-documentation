<!-- End user’s guide > Wrangler user guide > Transformation steps > Data anonymization steps > Add noise to number -->

##### Add noise to number

The **Add noise to number** step can be used to anonymize data in *integer* or *decimal* columns. This step generates a new random value that is within specified distance from the original value. See more details in [How are the new values calculated](wrangler-step-add-noise-to-number.md#how-are-the-new-values-calculated).

###### Parameters

- **Input column**: required, select a *decimal* or *integer* column.
- **Noise amount**: required, enter a **number** or **percentage** that will be used to calculate the range from which new random numbers is generated.
  - Default value *is 10%*.
- **Target column**: required, configure the column which will receive the output.
  - **Write result to the current column**: outputs data into the **Input column**.
  - **Create new column with name**: create a new column with the specified name. Name of the new column can contain spaces or special characters - the technical column name will be created automatically. The new column will be placed right next to the **Input column**.

###### How are the new values calculated

The step works by randomly generating a new value that is within the distance specified by the **Noise amount** parameter from the original value.

It works by calculating lower and upper bounds for the new value. These are both based on the **Noise amount** parameter:

- Lower bound is calculated as `$originalValue - noiseAmount` if the **Noise amount** is specified as absolute number or as `$originalValue * (100 - noiseAmount) / 100` if the **Noise amount** is specified as percentage value.
- Upper bound is calculated as `$originalValue + noiseAmount` if the **Noise amount** is specified as absolute number or as `$originalValue * (100 + noiseAmount) / 100` if the **Noise amount** is specified as percentage value.

Note that in both cases the algorithm properly accounts for values that either too large or too small and will not cause overflows.

Once the lower and upper bound is computed, a new random number is picked in the interval between those two values. This effectively means that you get a new random number that is never more than specified amount of time away from the original value.

###### Examples

| Original amount | Noise amount | Display format | Calculated range | Result amount |
| --- | --- | --- | --- | --- |
| 2000 | 10% | Any | ±200 (10% of 2000) | The result amount will be between `1800` and `2200`. |
| 2,000 | 400 | Any | ±400 | The result amount will be between `1600` and `2400`. |
| 99.99 | 10% | Not set | ±9.99 | The result amount will be between `90.0000000000` and `109.9800000000`. |
| 99.99 | 10% | #.## | ±9.99 | The result amount will be between `90.00` and `109.98`. |
| 0 | 10% | Any | 0 | The result amount will be `0`. |
| 0 | 10 | Any | ±10 | The result amount will be between `-10` and `10`. |
| *No value* | Any amount or percentage | Any | Not calculated | `No value` (the result is an empty value). |

###### Remarks

- New random values are generated with every job run.
- When adding noise to *decimal values*, the number of decimal places in the randomized values depends on the display format of the original column. See [Working with decimals](wrangler-faq.md#how-can-i-work-with-precise-numbers-including-currency) for more information on how to change the display format. When no display format is specified, the randomized numbers can have up to 10 decimal places.
- This step does not affect empty values (see [Working with empty values](wrangler-faq.md#how-do-i-work-with-empty-values-whats-the-difference-between-null-and-empty) for more information on empty values in Wrangler).

###### See also

- [Add noise to date step](wrangler-step-add-noise-to-date.md)
- [Mask text step](wrangler-step-mask-text.md)
- [`addNoise`](../developer/mathematical-functions-ctl2.md#addnoise) function.
