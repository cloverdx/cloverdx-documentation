<!-- End user’s guide > Wrangler user guide > Transformation steps > Math steps > Floor -->

##### Floor

**Floor** step rounds the number down to the nearest integer. Negative numbers are rounded away from zero while positive numbers are rounded towards zero.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| -2.1 | -3 | Negative numbers are rounded down away from zero. |
| 2.9 | 2 | Positive numbers are rounded down towards zero. |
| *No value* | *Error* | Calling **Floor** on an empty value results in an error. |

###### Remarks

- Applying the step to *No value* cells (cells containing *null*) will result in an error.

###### See also

- [Ceiling step](wrangler-step-ceiling.md) to round numbers down to the nearest integer.
- [Round step](wrangler-step-round.md) to round numbers to provided number of decimal places.
- [Truncate step](wrangler-step-truncate.md) to remove decimal portion of a number.
- [`floor`](../developer/mathematical-functions-ctl2.md#floor) function in CTL.
