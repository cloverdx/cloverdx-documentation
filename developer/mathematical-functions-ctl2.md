<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Mathematical functions -->

### Mathematical functions

#### List of functions

| [abs](mathematical-functions-ctl2.md#abs) |
| --- |
| [acos](mathematical-functions-ctl2.md#acos) |
| [addNoise](mathematical-functions-ctl2.md#addnoise) |
| [asin](mathematical-functions-ctl2.md#asin) |
| [atan](mathematical-functions-ctl2.md#atan) |
| [bitAnd](mathematical-functions-ctl2.md#bitand) |
| [bitIsSet](mathematical-functions-ctl2.md#bitisset) |
| [bitLShift](mathematical-functions-ctl2.md#bitlshift) |
| [bitNegate](mathematical-functions-ctl2.md#bitnegate) |
| [bitOr](mathematical-functions-ctl2.md#bitor) |
| [bitRShift](mathematical-functions-ctl2.md#bitrshift) |
| [bitSet](mathematical-functions-ctl2.md#bitset) |
| [bitXor](mathematical-functions-ctl2.md#bitxor) |
| [ceil](mathematical-functions-ctl2.md#ceil) |
| [cos](mathematical-functions-ctl2.md#cos) |
| [e](mathematical-functions-ctl2.md#e) |
| [exp](mathematical-functions-ctl2.md#exp) |
| [floor](mathematical-functions-ctl2.md#floor) |
| [log](mathematical-functions-ctl2.md#log) |
| [log10](mathematical-functions-ctl2.md#log10) |
| [max](mathematical-functions-ctl2.md#max) |
| [min](mathematical-functions-ctl2.md#min) |
| [pi](mathematical-functions-ctl2.md#pi) |
| [pow](mathematical-functions-ctl2.md#pow) |
| [random](mathematical-functions-ctl2.md#random) |
| [randomBoolean](mathematical-functions-ctl2.md#randomboolean) |
| [randomDecimal](mathematical-functions-ctl2.md#randomdecimal) |
| [randomGaussian](mathematical-functions-ctl2.md#randomgaussian) |
| [randomInteger](mathematical-functions-ctl2.md#randominteger) |
| [randomLong](mathematical-functions-ctl2.md#randomlong) |
| [round](mathematical-functions-ctl2.md#round) |
| [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven) |
| [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed) |
| [signum](mathematical-functions-ctl2.md#signum) |
| [sin](mathematical-functions-ctl2.md#sin) |
| [sqrt](mathematical-functions-ctl2.md#sqrt) |
| [tan](mathematical-functions-ctl2.md#tan) |
| [toDegrees](mathematical-functions-ctl2.md#todegrees) |
| [toRadians](mathematical-functions-ctl2.md#toradians) |

You may also want to use some mathematical functions:

#### abs

```ctl
integer abs(integer arg);
long abs(long arg);
number abs(number arg);
decimal abs(decimal arg);
```

The `abs()` function returns the absolute value of a given argument of numeric data type (`integer`, `long`, `number`, or `decimal`).

If the given argument is `null`, the function fails with an error.
> [!IMPORTANT]
> The `abs()` function behaves in the same way as the `abs()` function in Java or C/C++.
>
> For the minimal integer, it returns minimal `integer` value: `abs(-2147483648)` returns `-2147483648`.
>
> For the minimal long, it returns minimal `long` value: `abs(-9223372036854775808L)` returns `-9223372036854775808`

**Compatibility**

The `abs(integer)`, `abs(long)`, `abs(decimal)`, `abs(number)` functions are available since **CloverETL 3.0.0**.
Example 117. Usage of abs
The function `abs(-123)` returns `123` as integer.

The function `abs(-1234L)` returns `1234` as long.

The function `abs(-1234.5)` returns `1234.5` as number (double).

The function `abs(-1234.6D)` returns `1234.6` as decimal.

#### acos

```ctl
number acos(decimal angle);
number acos(number angle);
```

The `acos()` function returns arc cosine of an `angle`.

If a given argument is `null`, the function fails with an error.

**Compatibility**

The `acos(decimal|number)` function is available since **CloverETL 3.5.0-M2**.
Example 118. Usage of acos
The function `acos(0)` returns `1.5707963267948966`.

The function `acos(1L)` returns `0.0`.

The function `acos(sqrt(2)*0.5)` returns `0.7853981633974483`.

The function `acos(0.5D))` returns `1.0471975511965979`.

The function `acos(5)` returns `null`.

The function `toDegrees(acos(0.5))` returns `60`.

**See also:**[asin](mathematical-functions-ctl2.md#asin), [atan](mathematical-functions-ctl2.md#atan), [cos](mathematical-functions-ctl2.md#cos), [toDegrees](mathematical-functions-ctl2.md#todegrees)

#### addNoise

```ctl
integer addNoise(integer value, integer noise);
long addNoise(long value, long noise);
number addNoise(double value, double noise);
decimal addNoise(decimal value, decimal noise);
date addNoise(date value, long noise);
date addNoise(date value, long noise, unit timeunit);
```

The `addNoise()` function returns 'anonymized' value of the original value.

The parameter 'noise' allows to set ranges the return value can obtain - 'value +- noise'.
Example 119. Usage of addNoise
The function `addNoise(null, 10)` returns `null`.

The function `addNoise(1, 10)` returns value between `-9` and `11`.

The function `addNoise(2.5D, 0.5D)` returns value between `2.0` and `3.0`.

The function `addNoise(2023-01-01, 1, year)` returns value between `2022-01-01` and `2024-01-01`.

**See also:**[random](mathematical-functions-ctl2.md#random), [randomBoolean](mathematical-functions-ctl2.md#randomboolean), [randomGaussian](mathematical-functions-ctl2.md#randomgaussian), [randomInteger](mathematical-functions-ctl2.md#randominteger), [randomLong](mathematical-functions-ctl2.md#randomlong), [randomString](string-functions-ctl2.md#randomstring), [randomUUID](string-functions-ctl2.md#randomuuid), [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed)

#### asin

```ctl
number asin(decimal angle);
number asin(double angle);
```

The `asin()` function returns arc sine of an `angle`.

If the given argument is `null`, the function fails with an error.

**Compatibility**

The `asin()` function is available since **CloverETL 3.5.0-M2**.
Example 120. Usage of asin
The function `asin(0)` returns `0.0`.

The function `asin(1L)` returns `1.5707963267948966`.

The function `asin(sqrt(2)*0.5)` returns `0.7853981633974484`.

The function `asin(0.5D)` returns `0.5235987755982989`.

the function `asin(5)` returns `null`.

The function `toDegrees(asin(0.5))` returns `30`.

**See also:**[acos](mathematical-functions-ctl2.md#acos), [atan](mathematical-functions-ctl2.md#atan), [sin](mathematical-functions-ctl2.md#sin), [toDegrees](mathematical-functions-ctl2.md#todegrees)

#### atan

```ctl
number atan(decimal angle);
number atan(double angle);
```

The `atan()` function returns arc tangent of an `angle`.

If the given argument is `null`, the function fails with an error.

**Compatibility**

The `atan()` function is available since **CloverETL 3.5.0-M2**.
Example 121. Usage of atan
The function `atan(0)` returns `0.0`.

The function `atan(1L)` returns `0.7853981633974483`.

The function `atan(sqrt(3))` returns `0.7853981633974483`.

The function `atan(0.5D)` returns `0.4636476090008061`.

The function `toDegrees(atan(1))` returns `45`.

**See also:**[acos](mathematical-functions-ctl2.md#acos), [asin](mathematical-functions-ctl2.md#asin), [tan](mathematical-functions-ctl2.md#tan), [toDegrees](mathematical-functions-ctl2.md#todegrees)

#### bitAnd

```ctl
integer bitAnd(integer arg1, integer arg2);
long bitAnd(long arg1, long arg2);
byte bitAnd(byte arg1, byte arg2);
```

The `bitAnd()` function returns the number corresponding to the bitwise `and` of given integer, long or byte arguments.

For example, `bitAnd(11,7)` returns `3`. As decimal `11` can be expressed as bitwise `1011`, decimal `7` can be expressed as `111`, thus the result is `11` which corresponds to decimal `3`.

If one of the arguments is `long`, the function returns the `long` data type.

If one of the argument is `null`, the function fails with an error.

If the `byte` arguments are of different length, the length of returned `byte` is a minimum of the lengths of the arguments.

**Compatibility**

The `bitAnd(integer,integer)` and `bitAnd(long,long)` functions are available since **CloverETL 3.0.0**.

The `byte bitAnd(byte, byte)` function is available since **CloverETL 4.0.0-M2**.
Example 122. Usage of bitAnd
The function `bitAnd(6, 3)` returns `2` as `integer`.

The function `bitAnd(12L, 6L)` returns `4` as `long`.

The function `bitAnd(15L, 1)` returns `1` as `long`.

Let `b1 = hex2byte("4545")` and `b2 = hex2byte("464646")`. The function `bitAnd(b1, b2)` returns a result that can be displayed in hexa as `4444`.

**See also:**[bitIsSet](mathematical-functions-ctl2.md#bitisset), [bitLShift](mathematical-functions-ctl2.md#bitlshift), [bitNegate](mathematical-functions-ctl2.md#bitnegate), [bitOr](mathematical-functions-ctl2.md#bitor), [bitRShift](mathematical-functions-ctl2.md#bitrshift), [bitSet](mathematical-functions-ctl2.md#bitset), [bitXor](mathematical-functions-ctl2.md#bitxor), [byteAt](string-functions-ctl2.md#byteat),

#### bitIsSet

```ctl
boolean bitIsSet(integer arg, integer index);
boolean bitIsSet(long arg, integer index);
```

The `bitIsSet()` function determines the value of the bit of the first argument located on the `index` and returns `true` or `false`, if the bit is `1` or `0`, respectively.

If the index is greater than the number of bits in the data type, functions `bitIsSet(integer, integer)` and `bitIsSet(long, integer)` return `false`.

For example, `bitIsSet(11,3)` returns `true`. As decimal `11` can be expressed as bitwise `1011`, the bit whose index is 3 (the fourth from the right) is `1`, thus the result is `true`. And `bitIsSet(11,2)` would return `false`.

If one of the given arguments is `null`, the function fails with an error.

**Compatibility**

The `bitIsSet(integer,integer)` and `bitIsSet(long,integer)` functions are available since **CloverETL 3.0.0**.
Example 123. Usage of bitIsSet
The function `bitIsSet(19, 1)` returns `true`.

The function `bitIsSet(18, 0)` returns `false`.

The function `bitIsSet(18, 1)` returns `true`.

The function `bitIsSet(256, 8)` returns `true`.

**See also:**[bitAnd](mathematical-functions-ctl2.md#bitand), [bitLShift](mathematical-functions-ctl2.md#bitlshift), [bitNegate](mathematical-functions-ctl2.md#bitnegate), [bitOr](mathematical-functions-ctl2.md#bitor), [bitRShift](mathematical-functions-ctl2.md#bitrshift), [bitSet](mathematical-functions-ctl2.md#bitset), [bitXor](mathematical-functions-ctl2.md#bitxor), [byteAt](string-functions-ctl2.md#byteat),

#### bitLShift

```ctl
integer bitLShift(integer arg, integer shift);
long bitLShift(long arg, long shift);
```

The `bitLShift()` function returns the number corresponding to the original number with bits shifted to the left.

The new bits added to the number on the right side are set to 0. (`Shift` number of bits on the left side are added and set to `0`.) For example, `bitLShift(11,2)` returns `44`. As decimal `11` can be expressed as bitwise `1011`, thus the two bits on the right side (`00`) are added and the result is `101100` which corresponds to decimal `44`.

If one of the argument is `long`, the function returns the `long` data type.

If one of the argument is `null`, the function fails with an error.

**Compatibility**

The `bitLShift(integer,integer)` and `bitLShift(long,long)` functions are available since **CloverETL 3.0.0**.
Example 124. Usage of bitLShift
The function `bitLShift(4, 3)` returns `32`.

The function `bitLShift(4, 28)` returns `1073741824`.

The function `bitLShift(4, 29)` returns `null`.

The function `bitLShift(4, 29L)` returns `2147483648`.

The function `bitLShift(4L, 60)` returns `4611686018427387904`.

The function `bitLShift(5L, 61)` returns `-6917529027641081856`.

The function `bitLShift(4L, 61)` returns `null`.

**See also:**[bitAnd](mathematical-functions-ctl2.md#bitand), [bitIsSet](mathematical-functions-ctl2.md#bitisset), [bitNegate](mathematical-functions-ctl2.md#bitnegate), [bitOr](mathematical-functions-ctl2.md#bitor), [bitRShift](mathematical-functions-ctl2.md#bitrshift), [bitSet](mathematical-functions-ctl2.md#bitset), [bitXor](mathematical-functions-ctl2.md#bitxor), [byteAt](string-functions-ctl2.md#byteat),

#### bitNegate

```ctl
integer bitNegate(integer arg);
long bitNegate(long arg);
byte bitNegate(byte arg);
```

The `bitNegate()` function returns the number corresponding to its bitwise `inverted number`.

All ones are set up to zeros and all zeros are changed to ones.

If a given argument is `null`, the function fails with an error.

**Compatibility**

The `bitNegate(integer)` and `bitNegate(long)` functions are available since **CloverETL 3.0.0**.

The `bitNegate(byte)` function is available since **CloverETL 4.0.0-M2**.
Example 125. Usage of bitNegate
The function `bitNegate(11)` returns `-12`. The function inverts all bits in an argument. The result is `integer`.

The function `bitNegate(6L)` returns `-7`. The result value is `long`.

Let `b1 = hex2byte("989c9cdfd2a89e9393")`. The function `bitNegate(b1)` returns `676363202d57616c6c`.

**See also:**[bitAnd](mathematical-functions-ctl2.md#bitand), [bitIsSet](mathematical-functions-ctl2.md#bitisset), [bitLShift](mathematical-functions-ctl2.md#bitlshift), [bitOr](mathematical-functions-ctl2.md#bitor), [bitRShift](mathematical-functions-ctl2.md#bitrshift), [bitSet](mathematical-functions-ctl2.md#bitset), [bitXor](mathematical-functions-ctl2.md#bitxor), [byteAt](string-functions-ctl2.md#byteat),

#### bitOr

```ctl
integer bitOr(integer arg1, integer arg2);
long bitOr(long arg1, long arg2);
byte bitOr(byte arg1, byte arg2);
```

The `bitOr()` function returns the bitwise `or` of both arguments.

For example, `bitOr(11,7)` returns `15`. As decimal `11` can be expressed as bitwise `1011`, decimal `7` can be expressed as `111`, thus the result is `1111` which corresponds to decimal `15`.

If one of the given argument is `long`, the function returns the `long` data type.

If one of the given argument is `null`, the function fails with an error.

If the `byte` arguments are of different length, the length of returned `byte` is a minimum of the lengths of arguments.

**Compatibility**

The `bitOr(integer,integer)` and `bitOr(long,long)` functions are available since **CloverETL 3.0.0**.

The function `byte bitOr(byte, byte)` is available since **CloverETL 4.0.0-M2**.
Example 126. Usage of bitOr
The function `bitOr(6, 3)` returns `7` as `integer`.

The function `bitOr(12L, 6L)` returns `14` as `long`.

The function `bitOr(15L, 1)` returns `15` as `long`.

Let `b1 = hex2byte("4545")` and `b2 = hex2byte("464646")`. The function `bitOr(b1, b2)` returns a result that can be displayed in hexa as`4747`.

**See also:**[bitAnd](mathematical-functions-ctl2.md#bitand), [bitIsSet](mathematical-functions-ctl2.md#bitisset), [bitLShift](mathematical-functions-ctl2.md#bitlshift), [bitNegate](mathematical-functions-ctl2.md#bitnegate), [bitRShift](mathematical-functions-ctl2.md#bitrshift), [bitSet](mathematical-functions-ctl2.md#bitset), [bitXor](mathematical-functions-ctl2.md#bitxor), [byteAt](string-functions-ctl2.md#byteat),

#### bitRShift

```ctl
integer bitRShift(integer arg, integer shift);
long bitRShift(long arg, long shift);
```

The `bitRShift()` returns the number corresponding to the original number with bits shifted to the right.

`Shift` number of bits on the right side are removed. (For example, `bitRShift(11,2)` returns `2`.) As decimal `11` can be expressed as bitwise `1011`, thus the two bits on the right side are removed and the result is `10` which corresponds to decimal `2`.

If one of the given arguments is `long`, the function returns `long` data type.

If one of the given argument is `null`, the function fails with an error.

**Compatibility**

The `bitRshift(integer,integer)` and `bitRShift(long,long)` functions are available since **CloverETL 3.0.0**.
Example 127. Usage of bitRShift
The function `bitRShift(4, 2)`returns `1`.

The function `bitRShift(129L, 3)`returns `16`.

**See also:**[bitAnd](mathematical-functions-ctl2.md#bitand), [bitIsSet](mathematical-functions-ctl2.md#bitisset), [bitLShift](mathematical-functions-ctl2.md#bitlshift), [bitNegate](mathematical-functions-ctl2.md#bitnegate), [bitLShift](mathematical-functions-ctl2.md#bitlshift), [bitSet](mathematical-functions-ctl2.md#bitset), [bitXor](mathematical-functions-ctl2.md#bitxor), [byteAt](string-functions-ctl2.md#byteat),

#### bitSet

```ctl
integer bitSet(integer arg1, integer index, boolean setBitTo1);
long bitSet(long arg1, integer index, boolean setBitTo1);
```

The `bitSet()` function sets the value of the bit of the first argument located on the `index` specified as the second argument to `1` or `0` if the third argument is `true` or `false`, respectively, and returns the result as an integer or long.

If one of the given arguments is `null`, the function fails with an error.

**Compatibility**

The `bitSet(integer,integer,integer,boolean)` and `bitSet(long,long,long,boolean)` functions are available since **CloverETL 3.0.0**.
Example 128. Usage of bitSet
The function `bitSet(11,3,false)` returns `3`. As decimal `11` can be expressed as bitwise `1011`, the bit whose index is 3 (the fourth from the right) is set to `0`, thus the result is `11` which corresponds to decimal `3`.

The function `bitSet(11,2,true)` returns `1111` which corresponds to decimal `15`.

The function `bitSet(0,1,33)` returns `2`.

The function `bitSet(0,1,-23)` returns `512`.

The function `bitSet(0L,1,33)` returns `4294967296`.

**See also:**[bitAnd](mathematical-functions-ctl2.md#bitand), [bitIsSet](mathematical-functions-ctl2.md#bitisset), [bitLShift](mathematical-functions-ctl2.md#bitlshift), [bitNegate](mathematical-functions-ctl2.md#bitnegate), [bitLShift](mathematical-functions-ctl2.md#bitlshift), [bitRShift](mathematical-functions-ctl2.md#bitrshift), [bitXor](mathematical-functions-ctl2.md#bitxor)

#### bitXor

```ctl
integer bitXor(integer arg, integer arg);
long bitXor(long arg, long arg);
byte bitXor(byte arg, byte arg);
```

The `bitXor()` function returns the bitwise *exclusive or* of both arguments.

For example, `bitXor(11,7)` returns `12`. As decimal `11` can be expressed as bitwise `1011`, decimal `7` can be expressed as `111`, thus the result is `1100` which corresponds to decimal `15`.

If one of the given argument is `long`, the function returns the `long` data type.

If one of the given arguments is `null`, the function fails with an error.

If the `byte` arguments are of different length, the length of returned `byte` is a minimum of the lengths of arguments.

**Compatibility**

The `bitXor(integer,integer)` and `bitXor(long,long)` functions are available since **CloverETL 3.0.0**.

The `byte bitXor(byte,byte)` function is available since **CloverETL 4.0.0-M2**.
Example 129. Usage of bitXor
The function `bitXor(3, 7)` returns `4`.

The function `bitXor(4, 10L)` returns `14`.

Let `b1 = hex2byte("4545")` and `b2 = hex2byte("464646")`. The function `bitXor(b1, b2)` returns a result that can be displayed in hexa as `0303`.

**See also:**[bitAnd](mathematical-functions-ctl2.md#bitand), [bitIsSet](mathematical-functions-ctl2.md#bitisset), [bitLShift](mathematical-functions-ctl2.md#bitlshift), [bitNegate](mathematical-functions-ctl2.md#bitnegate), [bitLShift](mathematical-functions-ctl2.md#bitlshift), [bitRShift](mathematical-functions-ctl2.md#bitrshift), [bitSet](mathematical-functions-ctl2.md#bitset), [byteAt](string-functions-ctl2.md#byteat),

#### ceil

```ctl
decimal ceil(decimal arg);
number ceil(number arg);
```

The `ceil()` function returns the smallest (closest to negative infinity) value that is greater than or equal to the argument and is equal to a mathematical integer.

It returns `number` (double) for `integer`, `long` and `number`. It returns `decimal` for `decimal`.

If the given argument is `null`, the function fails with an error.

**Compatibility**

The `ceil(number)` and `ceil(decimal)` functions are available since **CloverETL 3.0.0**.

The function returns `number` for all input numeric data types in **CloverDX 3.4** and older.
Example 130. Usage of ceil
The function `ceil(-3.45D)` returns `-3.0`.

The function `ceil(3)` returns `3.0`.

The function `ceil(34L)` returns `34.0`.

The function `ceil(35.5)` returns `36.0`.

**See also:**[floor](mathematical-functions-ctl2.md#floor), [round](mathematical-functions-ctl2.md#round), [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

#### cos

```ctl
number cos(number angle);
number cos(decimal angle);
```

The `cos()` function returns the trigonometric cosine of a given `angle`.

Angle is in radians.

If the given argument is `null`, the function fails with an error.

**Compatibility**

The `cos(decimal)` and `cos(number)` functions are available since **CloverETL 3.5.0-M2**.
Example 131. Usage of cos
The function `cos(0.0D)` returns `1.0`.

The function `cos(pi()/4)` returns `0.7071067811865476`.

The function `cos(toRadians(30))` returns `0.5773502691896257`.

**See also:**[acos](mathematical-functions-ctl2.md#acos), [sin](mathematical-functions-ctl2.md#sin), [tan](mathematical-functions-ctl2.md#tan), [toRadians](mathematical-functions-ctl2.md#toradians)

#### e

```ctl
number e();
```

The `e()` function returns the Euler number.

**Compatibility**

The `e()` function is available since **CloverETL 3.0.0**.
Example 132. Usage of e The function `e()` returns `2.718281828459045`.
**See also:**[exp](mathematical-functions-ctl2.md#exp), [pi](mathematical-functions-ctl2.md#pi)

#### exp

```ctl
number exp(decimal arg);
number exp(integer arg);
number exp(long arg);
number exp(number arg);
```

The `exp()` function returns the result of the exponential function of the given argument.

The argument can be of any numeric data type (`integer`, `long`, `number`, or `decimal`).

If the given argument is `null`, the function fails with an error.

**Compatibility**

The `exp(decimal)` and `exp(number)` functions are available since **CloverETL 3.0.0**.
Example 133. Usage of exp
The function `exp(1)` returns `2.7182818284590455`.

The function `exp(0L)` returns `1.0`.

The function `exp(0.5D)` returns `1.6487212707001282`.

The function `exp(2.5)` returns `12.182493960703473`.

The function `exp(-5)` returns `0.006737946999085467`.

**See also:**[e](mathematical-functions-ctl2.md#e), [log](mathematical-functions-ctl2.md#log), [log10](mathematical-functions-ctl2.md#log10), [pow](mathematical-functions-ctl2.md#pow)

#### floor

```ctl
decimal floor(decimal arg);
number floor(number arg);
```

The `floor()` function returns the largest (closest to positive infinity) value that is less than or equal to the argument and is equal to a mathematical integer.

It returns `number` (double) for `integer`, `long` and `number` and it returns `decimal` for `decimal`.

If the given argument is `null`, the function fails with an error.

**Compatibility**

The `floor(decimal)` and `floor(number)` functions are available since **CloverETL 3.0.0**.

The function returns `number` for all input numeric data types in **CloverETL 3.4** and older.
Example 134. Usage of floor
The function `floor(5)` returns `5.0` as number (double).

The function `floor(-10L)` returns `-10.0` as number (double).

The function `floor(4.5D)` returns `4.00` as decimal.

The function `floor(-7.4)` returns `-8.0` as number (double).

**See also:**[ceil](mathematical-functions-ctl2.md#ceil), [round](mathematical-functions-ctl2.md#round), [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

#### log

```ctl
number log(decimal arg);
number log(number arg);
```

The `log()` function returns the result of the *natural logarithm* of a given argument.

If the given argument is `null`, the function fails with an error.

**Compatibility**

The `log(decimal)` and `log(number)` functions are available since **CloverETL 3.0.0**.
Example 135. Usage of log
The function `log(1)` returns `0.0`.

The function `log(10L)` returns `2.302585092994046`.

The function `log(4.5D)` returns `1.5040773967762742`.

The function `log(7.5)` returns `2.0149030205422647`.

The function `log(-7.4)` returns `NaN`.

The function `log(0)` returns `-Infinity`.

**See also:**[exp](mathematical-functions-ctl2.md#exp), [log10](mathematical-functions-ctl2.md#log10)

#### log10

```ctl
number log10(decimal arg);
number log10(number arg);
```

The `log10()` function returns the result of the logarithm of a given argument to the base 10.

If the given argument is `null`, the function fails with an error.

**Compatibility**

The `log10(decimal)` and `log10(number)` functions are available since **CloverETL 3.0.0**.
Example 136. Usage of log10
The function `log10(1)` returns `0.0`.

The function `log10(10L)` returns `1.0`.

The function `log10(7.5D)` returns `0.8750612633917001`.

The function `log10(0.5)` returns `-0.3010299956639812`.

The function `log10(0)` returns `-Infinity`.

The function `log10(-75)` returns `NaN`

**See also:**[log](mathematical-functions-ctl2.md#log), [pow](mathematical-functions-ctl2.md#pow)

#### max

```ctl
decimal max(decimal arg1, decimal arg2);
integer max(integer arg1, integer arg2);
long max(long arg1, long arg2);
number max(number arg1, number arg2);
<element type> max(<element type>[] list);
```

The `max()` function returns one of the given arguments which is bigger.

If one of the given arguments is `null`, the function returns the other argument. If both of the given arguments are `null`, the function returns `null`.

If a given list contains only `null` values or is empty, the function returns `null`. If the given list has a `null` reference, the function fails with an error. The returned element is the same data type as elements in the list.

**Compatibility**

The `max(integer, integer)`, `max(long,long)`, `max(number,number)`, `max(decimal,decimal)` and `max(E[])` functions are available since **CloverETL 3.5.0-M2**.
Example 137. Usage of max
The function `max(1, 2)` returns `2` as integer.

The function `max(3L, 4)` returns `4` as long.

The function `max(5.0, 8L)` returns `8` as number (double).

The function `max(5.25, 5.78D)` returns `5.78` as decimal.

The function `max(9, null)` returns `9`.

The list `ints` contains values `1, 3, 5, null, 4`. The functions `max(ints)` returns `5`.

The list `nulls` contains values `null, null, null, null`. The functions `max(nulls)` returns `null`.

**See also:**[min](mathematical-functions-ctl2.md#min)

#### min

```ctl
decimal min(decimal arg1, decimal arg2);
integer min(integer arg1, integer arg2);
long min(long arg1, long arg2);
number min(number arg1, number arg2);
<element type> min(<element type>[] list);
```

The `min()` function returns one of the given arguments which is smaller.

If one of the given arguments is `null`, the function returns the other argument. If both of the given arguments are `null`, the function returns `null`.

`Null` values in a list are omitted. The returned element is the same data type as elements in the list. If the given list contains only `null` values or is empty, the function returns `null`. If the given list has a `null` reference, the function fails with an error.

**Compatibility**

The `min(integer)`,`min(long)`, `min(number)`, `min(decimal)` and `min(E[])` functions are available since **CloverETL 3.5.0-M2**.
Example 138. Usage of min
The function `min(2, 1)` returns `1` as integer.

The function `min(2L, 7)` returns `2` as long.

The function `min(4.5, 7L)` returns `4.5` as number (double).

The function `min(4.75, 5.6D)` returns `4.75` as decimal.

The list `ints` contains values `1, 3, 5, null, 4`. The functions `min(ints)` returns `1`.

The list `nulls` contains values `null, null, null, null`. The functions `min(nulls)` returns `null`.

**See also:**[max](mathematical-functions-ctl2.md#max)

#### pi

```ctl
number pi();
```

The `pi` function returns the pi number.

**Compatibility**

The `pi()` function is available since **CloverETL 3.0.0**.
Example 139. Usage of pi The `pi()` function returns `3.141592653589793`.
**See also:**[e](mathematical-functions-ctl2.md#e)

#### pow

```ctl
decimal pow(decimal base, decimal exp);
number pow(number base, number exp);
```

The `pow()` function returns the exponential function of the first argument as the exponent with the second as the base.

The arguments can be of any numeric data type, data type do not need to be of the same type (`integer`, `long`, `number` or `decimal`).

If one of the given arguments is `null`, the function fails with an error.
> [!IMPORTANT]
> The function `pow` with `decimal` arguments uses the integer part of second argument only. Thus `pow(4D, 2.5D)` leads to a calculation of `pow(4D, 2D)`.

**Compatibility**

The `pow(decimal)`, `pow(number)`, `power(number,number)` and `pow(decimal,decimal)`. functions are available since **CloverETL 3.0.0**.
Example 140. Usage of pow
The function `pow(2L, 3)` returns `8.0` as number (double).

The function `pow(4, 3.5D)` returns `64.00` as decimal. The integer part of second argument is used. The result is same as a result of `pow(4, 3)`.

The function `pow(4, 3.5)` returns `128.0` as number (double).

The function `pow(2.7, 3.89)` returns `47.64365186615171` as number (double).

The function `pow(2, -1D)` fails.

The function `pow(2, -1)` returns `0.5` as number (double).

**See also:**[exp](mathematical-functions-ctl2.md#exp), [log](mathematical-functions-ctl2.md#log), [log10](mathematical-functions-ctl2.md#log10), [sqrt](mathematical-functions-ctl2.md#sqrt)

#### random

```ctl
number random();
number random(number minimum, number maximum);
```

The `random()` function generates random positive double greater than or equal to `0.0` and less than `1.0`.

If the range of allowed values is specified, the result value will be greater than or equal to `minimum` and lower than or equal to `maximum`.

If one of the given arguments is `null`, the function fails with an error.

**Compatibility**

The `random()` function is available since **CloverETL 3.0.0**.

The `random(number,number)` function is available since **CloverETL 6.4.0**.
Example 141. Usage of random The function `random()` returns for example `0.23096784138492643`. It can return another random value, e.g. 0.7559335772251974.
**See also:**[randomBoolean](mathematical-functions-ctl2.md#randomboolean), [randomDate](date-functions-ctl2.md#randomdate), [randomDecimal](mathematical-functions-ctl2.md#randomdecimal), [randomGaussian](mathematical-functions-ctl2.md#randomgaussian), [randomInteger](mathematical-functions-ctl2.md#randominteger), [randomLong](mathematical-functions-ctl2.md#randomlong), [randomString](string-functions-ctl2.md#randomstring), [randomUUID](string-functions-ctl2.md#randomuuid), [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed), [addNoise](mathematical-functions-ctl2.md#addnoise)

#### randomBoolean

```ctl
boolean randomBoolean();
```

The `randomBoolean()` function generates `true` or `false` boolean values at random.

If these values are sent to any numeric data type field, they are converted to their numeric representation automatically (`1` or `0`, respectively).

**Compatibility**

The `randomBoolean()` function is available since **CloverETL 3.0.0**.
Example 142. Usage of randomBoolean The function `randomBoolean()` returns `true` for example. It can return `false` too as the result is random.
**See also:**[random](mathematical-functions-ctl2.md#random), [randomDate](date-functions-ctl2.md#randomdate), [randomDecimal](mathematical-functions-ctl2.md#randomdecimal), [randomGaussian](mathematical-functions-ctl2.md#randomgaussian), [randomInteger](mathematical-functions-ctl2.md#randominteger), [randomLong](mathematical-functions-ctl2.md#randomlong), [randomString](string-functions-ctl2.md#randomstring), [randomUUID](string-functions-ctl2.md#randomuuid), [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed), [addNoise](mathematical-functions-ctl2.md#addnoise)

#### randomDecimal

```ctl
decimal randomDecimal();
decimal randomDecimal(decimal minimum, decimal maximum);
```

The `randomDecimal()` function generates random positive decimal greater than or equal to `0.0` and less than `1.0`.

If the range of allowed values is specified, the result value will be greater than or equal to `minimum` and lower than or equal to `maximum`.

If one of the given arguments is `null`, the function fails with an error.

**Compatibility**

The `randomDecimal()` and `randomDecimal(decimal, decimal)` functions are available since **CloverETL 6.4.0**.
Example 143. Usage of randomDecimal
The function `randomDecimal()` returns for example `0.23096784138492643`.

The function `randomDecimal(1D, 5D)` returns for example `2.35885588812358749`.

**See also:**[random](mathematical-functions-ctl2.md#random), [randomBoolean](mathematical-functions-ctl2.md#randomboolean), [randomDate](date-functions-ctl2.md#randomdate), [randomGaussian](mathematical-functions-ctl2.md#randomgaussian), [randomInteger](mathematical-functions-ctl2.md#randominteger), [randomLong](mathematical-functions-ctl2.md#randomlong), [randomString](string-functions-ctl2.md#randomstring), [randomUUID](string-functions-ctl2.md#randomuuid), [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed), [addNoise](mathematical-functions-ctl2.md#addnoise)

#### randomGaussian

```ctl
number randomGaussian();
```

The `randomGaussian()` function generates at random both positive and negative values of number data type in a Gaussian distribution.

The mean value is `0`. The standard deviation is `1`.

**Compatibility**

The `randomGausian()` function is available since **CloverETL 3.0.0**.
Example 144. Usage of randomGaussian The function `randomGaussian()` can return e.g. `-1.7478412353643376`.
**See also:**[random](mathematical-functions-ctl2.md#random), [randomBoolean](mathematical-functions-ctl2.md#randomboolean), [randomDate](date-functions-ctl2.md#randomdate), [randomDecimal](mathematical-functions-ctl2.md#randomdecimal), [randomInteger](mathematical-functions-ctl2.md#randominteger), [randomLong](mathematical-functions-ctl2.md#randomlong), [randomString](string-functions-ctl2.md#randomstring), [randomUUID](string-functions-ctl2.md#randomuuid), [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed), [addNoise](mathematical-functions-ctl2.md#addnoise)

#### randomInteger

```ctl
integer randomInteger();
integer randomInteger(integer minimum, integer maximum);
```

The `randomInteger()` function generates both positive and negative integer values at random.

If the range of allowed values is specified, the result value will be greater than or equal to `minimum` and lower than or equal to `maximum`.

If one of the given arguments is `null`, the function fails with an error.

**Compatibility**

The `randomInteger()` and `randomInteger(integer,integer)` functions are available since **CloverETL 3.0.0**.
Example 145. Usage of randomInteger
The function `randomInteger()` returns for example `-767954592`.

The function `randomInteger(0, 10)` returns for example `7`.

**See also:**[random](mathematical-functions-ctl2.md#random), [randomBoolean](mathematical-functions-ctl2.md#randomboolean), [randomDate](date-functions-ctl2.md#randomdate), [randomDecimal](mathematical-functions-ctl2.md#randomdecimal), [randomGaussian](mathematical-functions-ctl2.md#randomgaussian), [randomLong](mathematical-functions-ctl2.md#randomlong), [randomString](string-functions-ctl2.md#randomstring), [randomUUID](string-functions-ctl2.md#randomuuid), [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed), [addNoise](mathematical-functions-ctl2.md#addnoise)

#### randomLong

```ctl
long randomLong();
long randomLong(long minimum, long maximum);
```

The `randomLong()` function generates both positive and negative long values at random.

If the range of allowed values is specified, the result value will be greater than or equal to `minimum` and lower than or equal to `maximum`.

If one of the given arguments is `null`, the function fails with an error.

**Compatibility**

The `randomLong()` and `randomLong(long,long)` function is available since **CloverETL 3.0.0**.
Example 146. Usage of randomLong
The function `randomLong()` returns for example `-7985800599050861074`.

The function `randomLong(0, 5000000000L)` returns for example `4594415452`.

**See also:**[random](mathematical-functions-ctl2.md#random), [randomBoolean](mathematical-functions-ctl2.md#randomboolean), [randomDate](date-functions-ctl2.md#randomdate), [randomDecimal](mathematical-functions-ctl2.md#randomdecimal), [randomGaussian](mathematical-functions-ctl2.md#randomgaussian), [randomInteger](mathematical-functions-ctl2.md#randominteger), [randomString](string-functions-ctl2.md#randomstring), [randomUUID](string-functions-ctl2.md#randomuuid), [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed), [addNoise](mathematical-functions-ctl2.md#addnoise)

#### round

```ctl
decimal round(decimal arg);
long round(number arg);
integer round(integer arg, integer precision);
long round(long arg, integer precision);
number round(number arg, integer precision);
decimal round(decimal arg, integer precision);
```

The `round()` function returns a rounded value using the "half up" rounding mode: if both neighbors are equidistant, rounds up.

Positive `precision` denotes the number of places after the decimal point and negative precision stands for the number of places before the decimal point. Therefore it only makes sense to use negative precision for integer and long data type arguments, since it signals to round to tens, hundreds, thousands and so on. So `round(123, -2)` will result in `100` and `round(123.123, 2)` will result in `123.12`.

If the parameter `precision` is missing, the function rounds to nearest integer value.

If the given argument is `null`, the function fails with an error.

See also `roundHalfToEven(decimal, integer)`.

**Compatibility**

The `round(decimal)` and `round(number)` functions are available since **CloverETL 3.0.0**.

The `round(int)`, `round(long)`, `round(int,int)` and `round(long,int)` functions are available since **CloverETL 3.5.0-M2**.
Example 147. Usage of round
The function `round(2.5D)` returns `3.00` as decimal.

The function `round(4.5)` returns `5` as long.

The function `round(6.25D, 1)` returns `6.30` as decimal.

The function `round(6.25, 1)` returns `6.30` as number (double).

The function `round(-124556.78D, -3)` returns `-125000.00` as decimal.

The function `round(1253456.78, -6)` returns `10000000` as double.

**See also:**[ceil](mathematical-functions-ctl2.md#ceil), [floor](mathematical-functions-ctl2.md#floor), [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

#### roundHalfToEven

```ctl
decimal roundHalfToEven(decimal arg);
decimal roundHalfToEven(decimal arg, integer precision);
```

The `roundHalfToEven()` function returns decimal value rounded to the closest integer value.

Uses the "half to even" rounding mode (also called banker’s rounding), i.e. if both the neighbors are equidistant, rounds to the nearest even number.

If a given argument is `null`, the function fails with an error.

Positive `precision` denotes the number of places after the decimal point and negative precision stands for the number of places before the decimal point (tens, hundreds, thousands and so on).

**Compatibility**

The `roundHalfToEven(decimal)` and `roundHalfToEven(number)` functions are available since **CloverETL 3.5.0-M2**.
Example 148. Usage of roundHalfToEven
The function `roundHalfToEven(2.5D)` returns `2`.

The function `roundHalfToEven(3.5D)` returns `4`.

The function `roundHalfToEven(2.25D, 1)` returns `2.2`.

The function `roundHalfToEven(2.35D, 1)` returns `2.4`.

The function `roundHalfToEven(12.25D, -1)` returns `10.00`.

**See also:**[ceil](mathematical-functions-ctl2.md#ceil), [floor](mathematical-functions-ctl2.md#floor), [round](mathematical-functions-ctl2.md#round)

#### setRandomSeed

```ctl
void setRandomSeed(long arg);
```

The `setRandomSeed()` function generates the seed for all functions that generate values at random.

This function should be used in the `init()` function or method.

In such a case, all values generated at random do not change on different runs of the graph, they even remain the same after the graph is reset.

If the given argument is `null`, the function fails with an error.

The `setRandomSeed()` function sets random seed only for the CLT2 code of the component where it is used. It does not set the random seed for CTL2 functions in other components.

**Compatibility**

The `setRandomSeed(long)` function is available since **CloverETL 3.0.0**.
Example 149. Usage of setRandomSeed`function boolean init() { setRandomSeed(123456789012345678L); return true; }`
**See also:**[random](mathematical-functions-ctl2.md#random), [randomBoolean](mathematical-functions-ctl2.md#randomboolean), [randomDate](date-functions-ctl2.md#randomdate), [randomDecimal](mathematical-functions-ctl2.md#randomdecimal), [randomGaussian](mathematical-functions-ctl2.md#randomgaussian), [randomInteger](mathematical-functions-ctl2.md#randominteger), [randomLong](mathematical-functions-ctl2.md#randomlong), [randomString](string-functions-ctl2.md#randomstring), [randomUUID](string-functions-ctl2.md#randomuuid), [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed), [addNoise](mathematical-functions-ctl2.md#addnoise)

#### signum

```ctl
integer signum(integer arg);
long signum(long arg);
number signum(number arg);
integer signum(decimal arg);
```

The `signum()` function returns signum of the argument.

If the argument is negative, the function returns `-1`. If the argument is positive, the function returns `1`. It the argument is `0`, the function returns `0`.

If the argument is `null`, the function fails.

**Compatibility**

The `signum(integer)`, `signum(long)`, `signum(number)` and `signum(decimal)` functions are available since **CloverETL 3.5.0-M2**.
Example 150. Usage of signum
The function `signum(-2147483648)`returns `-1`.

The function `signum(-123456789012345L)` returns `-1`.

The function `signum(0.0)` returns `0`.

The function `signum(123.45d)` returns `1`.

The function `signum(null)` fails.

#### sin

```ctl
number sin(number angle);
number sin(decimal angle);
```

The `sin()` function returns the trigonometric sine of a given `angle`. The angle is in radians.

If the given argument is `null`, the function fails with an error.

**Compatibility**

The `sin(decimal)` and `sin(number)` functions are available since **CloverETL 3.5.0-M2**.
Example 151. Usage of sin
The function `sin(0D)` returns `0.0`.

The function `sin(pi()*0.5)` returns `1.0`.

The function `sin(toRadians(45))` returns `0.7071067811865475`.

**See also:**[asin](mathematical-functions-ctl2.md#asin), [cos](mathematical-functions-ctl2.md#cos), [tan](mathematical-functions-ctl2.md#tan), [toRadians](mathematical-functions-ctl2.md#toradians)

#### sqrt

```ctl
number sqrt(number arg);
number sqrt(decimal arg);
```

The `sqrt()` function returns the square root of a given argument.

The argument can be of any numeric data type; if the argument is `integer` or `long`, the argument will be converted to the `number``(double)`.

If a given argument is `null`, the function fails with an error.

**Compatibility**

The `sqrt(decimal)` and `sqrt(number)` functions are available since **CloverETL 3.0.0**.
Example 152. Usage of sqrt
The function `sqrt(81)` returns `9.0`.

The function `sqrt(40532396646334464L)` returns `2.01326592E8`.

The function `sqrt(1.21)` returns `1.1`.

The function `sqrt(1.44D)` returns `1.2`.

The function `sqrt(0)` returns `0.0`.

the function `sqrt(-1)` returns `null`.

**See also:**[log](mathematical-functions-ctl2.md#log), [log10](mathematical-functions-ctl2.md#log10), [pow](mathematical-functions-ctl2.md#pow)

#### tan

```ctl
number tan(number angle);
number tan(decimal angle);
```

The `tan()` function returns the trigonometric tangent of a given `angle`. The angle is in radians.

If the given argument is `null`, the function fails with an error.

**Compatibility**

The `tan(decimal)` and `tan(number)` functions are available since **CloverETL 3.5.0-M2**.
Example 153. Usage of tan
The function `tan(0.0D)` returns `0.0`.

The function `tan(pi()/3)` returns `1.7320508075688767`.

The function `tan(toRadians(30))` returns `0.5773502691896257`.

**See also:**[atan](mathematical-functions-ctl2.md#atan), [cos](mathematical-functions-ctl2.md#cos), [sin](mathematical-functions-ctl2.md#sin), [toRadians](mathematical-functions-ctl2.md#toradians)

#### toDegrees

```ctl
double toDegrees(double angle);
double toDegrees(decimal angle);
```

The `toDegrees` function converts radians to degrees.

The `angle` is in radians. If the angle is `null`, the function fails.

**Compatibility**

The `toDegrees(decimal)` and `toDegrees(number)` functions are available since **CloverETL 3.5.0-M2**.
Example 154. Usage of toDegrees
The function `toDegrees(0)` returns `0.0`.

The function `toDegrees(pi())` returns `180.0`.

**See also:**[acos](mathematical-functions-ctl2.md#acos), [asin](mathematical-functions-ctl2.md#asin), [atan](mathematical-functions-ctl2.md#atan), [toRadians](mathematical-functions-ctl2.md#toradians)

#### toRadians

```ctl
double toRadians(double angle);
double toRadians(decimal angle);
```

The `toRadians` function converts degrees to radians.

The `angle` is in degrees. If the `angle` is `null`, the function fails.

**Compatibility**

The `toRadians(decimal)` and `toRadians(number)` functions are available since **CloverETL 3.5.0-M2**.
Example 155. Usage of toRadians
The function `toRadians(0)` returns `0`.

The function `toRadians(90d)` returns `1.5707963267948966`.

**See also:**[cos](mathematical-functions-ctl2.md#cos), [sin](mathematical-functions-ctl2.md#sin), [tan](mathematical-functions-ctl2.md#tan), [toDegrees](mathematical-functions-ctl2.md#todegrees)
