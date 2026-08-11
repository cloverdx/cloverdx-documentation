<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Date functions -->

### Date functions

#### List of functions

| [createDate](date-functions-ctl2.md#createdate) |
| --- |
| [dateAdd](date-functions-ctl2.md#dateadd) |
| [dateDiff](date-functions-ctl2.md#datediff) |
| [extractDate](date-functions-ctl2.md#extractdate) |
| [extractTime](date-functions-ctl2.md#extracttime) |
| [getYear](date-functions-ctl2.md#getyear) |
| [getMonth](date-functions-ctl2.md#getmonth) |
| [getDay](date-functions-ctl2.md#getday) |
| [getHour](date-functions-ctl2.md#gethour) |
| [getMinute](date-functions-ctl2.md#getminute) |
| [getSecond](date-functions-ctl2.md#getsecond) |
| [getMillisecond](date-functions-ctl2.md#getmillisecond) |
| [getDayOfWeek](date-functions-ctl2.md#getdayofweek) |
| [randomDate](date-functions-ctl2.md#randomdate) |
| [today](date-functions-ctl2.md#today) |
| [zeroDate](date-functions-ctl2.md#zerodate) |
| [trunc](date-functions-ctl2.md#trunc) |
| [truncDate](date-functions-ctl2.md#truncdate) |

When you work with a date, you may use functions that process dates.

In these functions, sometimes a format pattern of a date or any number must be defined. Also a locale and time zone can have an influence on their formatting.

- For detailed information about the date formatting and/or parsing, see [Date and Time Format](metadata-records-and-fields.md#date-and-time-format).
- For detailed information about locale, see [Locale](metadata-records-and-fields.md#locale).
- For detailed information about time zones, see [Time Zone](metadata-records-and-fields.md#timezone).
> [!NOTE]
> Remember that numeric and date formats are displayed using the system value **Locale** or **Locale** specified in the `defaultProperties` file, unless other **Locale** is explicitly specified. Similarly for **Time zone**.
>
> For more information on how **Locale** and **Time zone** may be changed in the `defaultProperties`, see [Engine configuration](../admin/designer-configuration.md#engine-configuration).

Here we provide the list of the functions:

#### createDate

```ctl
date createDate(integer year, integer month, integer day);
date createDate(integer year, integer month, integer day, string timeZone);
date createDate(integer year, integer month, integer day, integer hour, integer minute, integer second);
date createDate(integer year, integer month, integer day, integer hour, integer minute, integer second, string timeZone);
date createDate(integer year, integer month, integer day, integer hour, integer minute, integer second, integer millisecond);
date createDate(integer year, integer month, integer day, integer hour, integer minute, integer second, integer millisecond, string timeZone);
```

The function `createDate()` creates a date using provided year, month (numbered from 1), day of month, hour, minute, second, millisecond and time zone.

If any of the above mentioned parameters is missing, value is set to zero. If the time zone is missing, the default time zone is used.

If one or more of specified parameters is `null`, the function fails.

**Compatibility**

The functions `createDate(integer,integer,integer)`, `createDate(integer,integer,integer,string)`, `createDate(integer,integer,integer,integer,integer,integer)`, `createDate(integer,integer,integer,integer,integer,integer,integer)`, `createDate(integer,integer,integer,integer,integer,integer,string)` and `createDate(integer,integer,integer,integer,integer,integer,string)` are available since **CloverETL 3.5.0-M1**.
Example 102. Usage of createDate
The function `createDate(2013, 7, 31)` returns a date corresponding to the 31 July 2013 0:00 using the default time zone. The summer/winter time is taken into account. For example, the expression returns `30 July 2013 22:00 GMT` in time zone `GMT+1` using the summer time.

The function `createDate(2013, 10, 4, "GMT+3")` returns `4 October 2013 0:00 GMT+3`. It is the same as `3 October 2013 21:00 GMT+0`.

The function `createDate(2009, 2, 13, 23, 31, 30)` returns `13 February 2009 23:31:30` in the default time zone. For example the expression corresponds to `13 February 2009 22:31:30 GMT` if the default time zone is `GMT+1`.

The function `createDate(2009, 2, 13, 23, 31, 30, "GMT-1")` returns `14 February 2009 0:31:30 GMT`.

The function `createDate(2009, 2, 13, 23, 31, 30, 123)` returns `13 February 2009 23:31:30.123` in the default time zone. For example the expression corresponds to `13 February 2009 22:31:30.123 GMT` if the default time zone is `GMT+1`.

The function `createDate(2009, 2, 13, 23, 31, 30, 124, "GMT-1")` returns `14 February 2009 0:31:30.124 GMT`

**See also:**[str2date](conversion-functions-ctl2.md#str2date)

#### dateAdd

```ctl
date dateAdd(date arg, long amount, unit timeunit);
```

The `dateAdd()` function adds a number of time units to the date and returns a new date.

Parameter `arg` is the date to which the number of time units is added.

Parameter `amount` defines the number of units to be added.

The `unit` parameter defines the unit of the second function parameter. The `unit` argument can be one of the following: `year`, `month`, `week`, `day`, `hour`, `minute`, `second`, `millisec`. The unit must be specified as a constant. It can neither be received through an edge nor set as a variable.

The function returns the new resulting date.

If one of the arguments is `null`, the function fails with an error.

**Compatibility**

The `dateAdd(date,long,timeunit)` function is available since **CloverETL 3.0.0**.
Example 103. Usage of dateAdd
Let us set up `date d` to 13 February 2009 23:31:30 GMT.

The function `dateAdd(d, 1, year)` returns `2010-02-13 23:31:30 GMT`.

The function `dateAdd(d, 1, month)` returns `2009-03-13 23:31:30 GMT`.

The function `dateAdd(d, 1, day)` returns `2009-02-14 23:31:30 GMT`.

The `czDate` is `30.3.2014 00:00:00` in the time zone `Europe/Prague`.

The function `dateAdd(czDate, 24, hour)` returns `31.3.2014 01:00:00 CEST`.

The function `dateAdd(czDate, 1, day)` returns `31.3.2014 00:00:00 CEST`

The `ukDate` is `2014-03-30 00:20:00` in the time zone `Europe/London`.

The function `dateAdd(ukDate, 41, minute)` returns `2014-04 02:01:00` in the time zone `Europe/London`.

The function `dateAdd(ukDate, 1, hour)` returns `2014-03-30 02:20:00` in the time zone `Europe/London`.

The function `dateAdd(ukDate, 1, day)` returns `2014-03-31 00:20:00` in the time zone `Europe/London`.

**See also:**[createDate](date-functions-ctl2.md#createdate), [dateDiff](date-functions-ctl2.md#datediff)

#### dateDiff

```ctl
long dateDiff(date later, date earlier, unit timeunit);
```

The `dateDiff()` function returns the difference of two date variables in a specified time units.

The `later` and `earlier` parameters represent a later and earlier date respectively.

The difference of two dates is expressed in defined time units. The `unit` can be one of the following: `year`, `month`, `week`, `day`, `hour`, `minute`, `second`, `millisec`. The unit must be specified as a constant. It can be neither received through an edge nor set as variable.
> [!IMPORTANT]
> If the `unit` is `hour`, `minute`, `second` or `millisec`, it counts the difference in the same way as it would be measured using *stopclock*. If the `unit` is `day`, `month` or `year`, the difference affected by winter/summer time turn is calculated differently. See examples.

The result is a `long` number. The result of the function is truncated: two date variables with a difference of `40` hours yield a difference of `1` days.

If one of the given argument is `null`, the function fails with an error.
> [!IMPORTANT]
> *Be aware that adjusting for the daylight saving time* - winter/summer time affects the results of `dateDiff()`.
>
> Different countries switch between summer time and winter time on different days.
>
> The function `dateDiff()` uses the time zone of your operating system.

**Compatibility**

The `dateDiff(date,date,timeunit)` function is available since **CloverETL 3.0.0**.
Example 104. Usage of dateDiff
The function `dateDiff(2008-06-18, 2001-02-03, year)` returns `7`. But, `dateDiff(2001-02-03, 2008-06-18, year)` returns `-7`.

Let’s call `2009-02-13 23:31:30 GMT+0` as `d1` and `2011-01-10 20:12:33` as `d2`.

The function `dateDiff(d2, d1, year)` returns `1`.

The function `dateDiff(d2, d1, month)` returns `22`.

The function `dateDiff(d2, d1, day)` returns `695`.

The variable `L2` is `2014-03-30 02:01:00` in the time zone `Europe/London`. The variable `L1` is `2014-03-30 00:59:00` in the time zone `Europe/London`. The function `dateDiff(L2, L1, minute)`returns `2`.

Set `2014-03-30 00:15:00` with the time zone `Europe/London` as `london1` and set `2014-03-30 02:15:00` with the same time zone as `london2`. The function `dateDiff(london2, london1, hour)` returns `1`.

Set `2014-03-30 00:15:00` with the time zone `America/New_York` as `ny1` and set `2014-03-30 02:15:00` with the same time zone as `ny2`. The function `dateDiff(ny2, ny1, hour)` returns `2`.

Set `2014-02-10 10:15:00` with the time zone `America/New_York` as `nyFeb10` and `2014-02-10 10:15:00` with the time zone `Europe/London` as `ukFeb10`. The function `dateDiff(nyFeb10, ukFeb10, hour)` returns `5`.

Set `2014-03-10 10:15:00` with the time zone `America/New_York` as `nyMar10` and `2014-03-10 10:15:00` with the time zone `Europe/London` as `ukMar10`. The function `dateDiff(nyMar10, ukMar10, hour)` returns `4`.

Set `2014-03-08 12:14:16` with the time zone `America/New_York` as `ny21` and `2014-03-09 12:14:16` with the same time zone as `ny22`.

The function `dateDiff(ny22, ny21, millisec)` returns `82800000`.

The function `dateDiff(ny22, ny21, second)` returns `82800`.

The function `dateDiff(ny22, ny21, minute)` returns `1380`.

The function `dateDiff(ny22, ny21, hour)` returns `23`.

The function `dateDiff(ny22, ny21, day)` returns `1` if processing runs on machine with the same time zone as the data (`America/New_York`). The function returns `0` if processing runs on machine with a different time zone (e.g. `Europe/London`). Time in the time zone `Europe/London` is turned on the different day than in time zones in US. If you would process data having the time zone `America/New_York` using the time zone `America/Los_Angeles`, you would get `0` or `1`.

**See also:**[dateAdd](date-functions-ctl2.md#dateadd), [str2date](conversion-functions-ctl2.md#str2date)

#### extractDate

```ctl
date extractDate(date arg);
```

The `extractDate` function takes a date argument and returns only the information containing year, month, and day values. The function’s argument is not modified by the return value.

If the input argument is `null`, the function returns `null`.

The default locale and default time zone are applied.

**Compatibility**

The `extractDate(date)` function is available since **CloverETL 3.0.0**.
Example 105. Usage of extractDate
Let’s call 13 February 2009 23:31:30 GMT+0 as `d`.

The function `extractDate(d)` returns `2009-02-13 0:00:00 GMT+0` provided the default time zone is GMT+0. If the default time zone is GMT+1, the function will return `2009-02-14 0:00:00 GMT+1`. (The result corresponds to `2009-02-13 23:00:00 GMT+0`.)

**See also:**[extractTime](date-functions-ctl2.md#extracttime), [str2date](conversion-functions-ctl2.md#str2date)

#### extractTime

```ctl
date extractTime(date arg);
```

The `extractTime()` function takes a date argument and returns only the information containing hours, minutes, seconds, and milliseconds. The function’s argument is not modified by the return value.

If the input argument is `null`, the function returns `null`.

The default locale and default time zone are applied.

**Compatibility**

The `extractTime(date)` function is available since **CloverETL 3.0.0**.
Example 106. Usage of extractTime
Let’s call 13 February 2009 23:31:30 GMT+0 as `d`.

The function `extractTime(d)` returns `23:31:30` provided the default time zone is GMT+0. If the default time zone is GMT+1, the function will return `0:31:30`.

**See also:**[extractDate](date-functions-ctl2.md#extractdate), [str2date](conversion-functions-ctl2.md#str2date)

#### getYear

```ctl
integer getYear(date arg);
integer getYear(date arg, string timeZone);
```

The `getYear()` function returns the year of `arg`.

If the argument is `null`, the function returns `null`.

If the `timeZone` argument is `null` or the argument is missing, the function uses the default [Time Zone](metadata-records-and-fields.md#timezone).

**Compatibility**

The `getYear(date)` and `getYear(date,string)` functions are available since **CloverETL 3.5.0-M1**.
Example 107. Usage of getYear
Let’s call 2011-01-01 1:05:00 GMT as `d`.

The function `getYear(d)` returns `2011`. The default time zone is used.

The function `getYear(d, "GMT+0")` returns `2011`.

the function `getYear(d, "GMT-3")` returns `2010`. There have not been a midnight in the `GMT-3` yet.

**See also:**[date2str](conversion-functions-ctl2.md#date2str), [getMonth](date-functions-ctl2.md#getmonth), [getDay](date-functions-ctl2.md#getday), [getHour](date-functions-ctl2.md#gethour), [getMinute](date-functions-ctl2.md#getminute), [getSecond](date-functions-ctl2.md#getsecond), [getMillisecond](date-functions-ctl2.md#getmillisecond), [getDayOfWeek](date-functions-ctl2.md#getdayofweek), [str2date](conversion-functions-ctl2.md#str2date)

#### getMonth

```ctl
integer getMonth(date arg);
integer getMonth(date arg, string timeZone);
```

The `getMonth()` function returns the month of the year (numbered from 1) of `arg`.

If the argument is `null`, the function returns `null`.

If the `timeZone` argument is `null` or the argument is missing, the function uses the default [Time Zone](metadata-records-and-fields.md#timezone).

**Compatibility**

The `getMonth(date)` and `getMonth(date,string)` functions are available since **CloverETL 3.5.0-M1**.
Example 108. Usage of getMonth
Let’s call 2011-01-01 1:05:00 GMT as `d`.

The function `getMonth(d)` returns `1` provided the default time zone is `GMT+1`.

The function `getMonth(d, "GMT+0")` returns `1`.

The function `getMonth(d, "GMT-3")` returns `12`. There have not been a midnight in the `GMT-3` yet.

**See also:**[date2str](conversion-functions-ctl2.md#date2str), [getYear](date-functions-ctl2.md#getyear), [getDay](date-functions-ctl2.md#getday), [getHour](date-functions-ctl2.md#gethour), [getMinute](date-functions-ctl2.md#getminute), [getSecond](date-functions-ctl2.md#getsecond), [getMillisecond](date-functions-ctl2.md#getmillisecond), [getDayOfWeek](date-functions-ctl2.md#getdayofweek), [str2date](conversion-functions-ctl2.md#str2date)

#### getDay

```ctl
integer getDay(date arg);
integer getDay(date arg, string timeZone);
```

The `getDay()` function returns the day of the month of `arg`.

If the argument is `null`, the function returns `null`.

If the `timeZone` argument is `null` or the time zone argument is not present, the function uses the default [Time Zone](metadata-records-and-fields.md#timezone).

**Compatibility**

The `getDay(date)` and `getDay(date,string)` functions are available since **CloverETL 3.5.0-M1**.
Example 109. Usage of getDay
Let’s call 2011-01-01 1:05:00 GMT as `d`.

The function `getDay(d)` returns `1` provided the default time zone is `GMT+1`.

The function `getDay(d, "GMT+0")` returns `1`.

The function `getDay(d, "GMT-3")` returns `31`. There have not been a midnight in the `GMT-3` yet.

**See also:**[date2str](conversion-functions-ctl2.md#date2str), [getYear](date-functions-ctl2.md#getyear), [getMonth](date-functions-ctl2.md#getmonth), [getHour](date-functions-ctl2.md#gethour), [getMinute](date-functions-ctl2.md#getminute), [getSecond](date-functions-ctl2.md#getsecond), [getMillisecond](date-functions-ctl2.md#getmillisecond), [getDayOfWeek](date-functions-ctl2.md#getdayofweek), [str2date](conversion-functions-ctl2.md#str2date)

#### getHour

```ctl
integer getHour(date arg);
integer getHour(date arg, string timeZone);
```

The `getHour()` function returns the hour of the day (24-hour clock) of `arg`.

If the argument is `null`, the function returns `null`. Otherwise the specified time zone is used.

If the `timeZone` argument is `null`, the function uses the default [Time Zone](metadata-records-and-fields.md#timezone).

**Compatibility**

The `getHour(date)` and `getHour(date)` functions are available since **CloverETL 3.5.0-M1**.
Example 110. Usage of getHour
Let’s call 2011-01-01 1:05:00 GMT as `d`.

The function `getHour(d)` returns `2` provided the default time zone is `GMT+1`.

The function `getHour(d, "GMT+0")` returns `1`.

The function `getHour(d, "GMT-3")` returns `22`.

**See also:**[date2str](conversion-functions-ctl2.md#date2str), [getYear](date-functions-ctl2.md#getyear), [getMonth](date-functions-ctl2.md#getmonth), [getDay](date-functions-ctl2.md#getday), [getMinute](date-functions-ctl2.md#getminute), [getSecond](date-functions-ctl2.md#getsecond), [getMillisecond](date-functions-ctl2.md#getmillisecond), [getDayOfWeek](date-functions-ctl2.md#getdayofweek), [str2date](conversion-functions-ctl2.md#str2date)

#### getMinute

```ctl
integer getMinute(date arg);
integer getMinute(date arg, string timeZone);
```

The `getMinute()` function returns the minute of the hour of `arg`.

If the argument is `null`, the function returns `null`.

If the `timeZone` argument is `null` or the parameter is not present, the function uses the default [Time Zone](metadata-records-and-fields.md#timezone).

**Compatibility**

The `getMinute(date)` and `getMinute(date,string)` functions are available since **CloverETL 3.5.0-M1**.
Example 111. Usage of getMinute
Let’s call 2011-01-01 1:05:00 GMT as `d`.

The function `getMinute(d)` returns `5`, provided the default time zone is `GMT+1`.

The function `getMinute(d, "GMT+0")` returns `5`.

the function `getMinute(d, "GMT-9:30")` returns `35`.

**See also:**[date2str](conversion-functions-ctl2.md#date2str), [getYear](date-functions-ctl2.md#getyear), [getMonth](date-functions-ctl2.md#getmonth), [getDay](date-functions-ctl2.md#getday), [getHour](date-functions-ctl2.md#gethour), [getSecond](date-functions-ctl2.md#getsecond), [getMillisecond](date-functions-ctl2.md#getmillisecond), [getDayOfWeek](date-functions-ctl2.md#getdayofweek), [str2date](conversion-functions-ctl2.md#str2date)

#### getSecond

```ctl
integer getSecond(date arg);
integer getSecond(date arg, string timeZone);
```

The `getSecond()` function returns the second of the minute of `arg`.

If the argument is `null`, the function returns `null`.

If the `timeZone` argument is `null` or the argument in not present, the function uses the default [Time Zone](metadata-records-and-fields.md#timezone).

**Compatibility**

The `getSecond(date)` and `getSecond(date,string)` functions are available since **CloverETL 3.5.0-M1**.
Example 112. Usage of getSecond
Let’s call 2011-01-01 1:05:02 GMT as `d`.

The function `getSecond(d)` returns `2`.

The function `getSecond(d, "GMT+0")` returns `2`.

the function `getSecond(d, "GMT-4")` returns `2`.

**See also:**[date2str](conversion-functions-ctl2.md#date2str), [getYear](date-functions-ctl2.md#getyear), [getMonth](date-functions-ctl2.md#getmonth), [getDay](date-functions-ctl2.md#getday), [getHour](date-functions-ctl2.md#gethour), [getMinute](date-functions-ctl2.md#getminute), [getMillisecond](date-functions-ctl2.md#getmillisecond), [getDayOfWeek](date-functions-ctl2.md#getdayofweek), [str2date](conversion-functions-ctl2.md#str2date)

#### getMillisecond

```ctl
integer getMillisecond(date arg);
integer getMillisecond(date arg, string timeZone);
```

The `getMillisecond()` function returns the millisecond of the second of `arg`.

If the argument is `null`, the function returns `null`.

If the `timeZone` argument is `null` or the parameter is not present, the function uses the default [Time Zone](metadata-records-and-fields.md#timezone).

**Compatibility**

The `getMillisecond(date)` and `getMillisecond(date,string)` functions are available since **CloverETL 3.5.0-M1**.
Example 113. Usage of getMillisecond
Let’s call 2011-01-01 1:05:02.123 GMT as `d`.

The function `getMillisecond(d)` returns `123`.

The function `getMillisecond(d, "GMT+0")` returns `123`.

the function `getMillisecond(d, "GMT-4")` returns `123`.

**See also:**[date2str](conversion-functions-ctl2.md#date2str), [getYear](date-functions-ctl2.md#getyear), [getMonth](date-functions-ctl2.md#getmonth), [getDay](date-functions-ctl2.md#getday), [getHour](date-functions-ctl2.md#gethour), [getMinute](date-functions-ctl2.md#getminute), [getSecond](date-functions-ctl2.md#getsecond), [getDayOfWeek](date-functions-ctl2.md#getdayofweek), [str2date](conversion-functions-ctl2.md#str2date)

#### getDayOfWeek

```ctl
integer getDayOfWeek(date arg);
integer getDayOfWeek(date arg, string timeZone);
```

The `getDayOfWeek()` function returns the day of the week (Monday = 1 …​ Sunday = 7) of `arg`.

If the argument is `null`, the function returns `null`.

If the `timeZone` argument is `null` or the time zone argument is not present, the function uses the default [Time Zone](metadata-records-and-fields.md#timezone).

**Compatibility**

The `getDayOfWeek(date)` and `getDayOfWeek(date,string)` functions are available since **CloverDX 6.5**.
Example 114. Usage of getDayOfWeek
Let’s call 2024-01-01 1:05:00 GMT as `d`.

The function `getDayOfWeek(d)` returns `1` provided the default time zone is `GMT+1`.

The function `getDayOfWeek(d, "GMT+0")` returns `1`.

The function `getDayOfWeek(d, "GMT-3")` returns `7`. There have not been a midnight in the `GMT-3` yet.

**See also:**[date2str](conversion-functions-ctl2.md#date2str), [getYear](date-functions-ctl2.md#getyear), [getMonth](date-functions-ctl2.md#getmonth), [getDay](date-functions-ctl2.md#getday), [getHour](date-functions-ctl2.md#gethour), [getMinute](date-functions-ctl2.md#getminute), [getSecond](date-functions-ctl2.md#getsecond), [getMillisecond](date-functions-ctl2.md#getmillisecond), [str2date](conversion-functions-ctl2.md#str2date)

#### randomDate

```ctl
date randomDate(date startDate, date endDate);
date randomDate(long startDate, long endDate);
date randomDate(string startDate, string endDate, string format);
date randomDate(string startDate, string endDate, string format, string locale);
date randomDate(string startDate, string endDate, string format, string locale, string timeZone);
```

The `randomDate()` function returns a random date between `startDate` and `endDate`.

These resulting dates are generated at random for different records and different fields. They can be different for both records and fields. The return value can also be `startDate` or `endDate`. However, it cannot be the date before `startDate` nor after `endDate`.

If one of the given dates is `null`, the function fails with an error.

If the `format` is `null` or the function does not have the `format` parameter, the default value is used.

If the `timezone` is `null` or the function does not have the `timezone` parameter, the default [Time Zone](metadata-records-and-fields.md#timezone) is used.

If the `locale` is `null` or the field is missing, the default [Locale](metadata-records-and-fields.md#locale) is used.

**Compatibility**

The `randomDate(long,long)`, `randomDate(date,date)`, `randomDate(string,string,string,string)` and `randomDate(string,string,string)` functions are available since **CloverETL 3.0.0**.

The function `randomDate(string,string,string,string,string)` is available since **CloverETL 3.5.0-M1**.
Example 115. Usage of randomDate
Let’s call `2011-01-01 0:00:00` as `date1` and `2012-01-01 0:00:00` as `date2`. The function `randomDate(date1, date2)` returns for example `2011-06-19`.

The function `randomDate(123456789000L, 1266103890000L)` returns for example `2009-06-20`.

The function `randomDate("2011-11-11", "2012-12-12", "yyyy-MM-dd")` returns for example `2012-09-01`.

The function `randomDate("10 octobre 2011", "11 novembre 2011", "dd MMMM yyyy", "fr.FR")` returns for example `2011-10-14`.

The function `randomDate("2011-01-11", "2011-08-12", "yyyy-MM-dd", "en.US", "GMT-5")` returns for example `2011-05-14`.

**See also:**[random](mathematical-functions-ctl2.md#random), [randomBoolean](mathematical-functions-ctl2.md#randomboolean), [randomGaussian](mathematical-functions-ctl2.md#randomgaussian), [randomInteger](mathematical-functions-ctl2.md#randominteger), [randomLong](mathematical-functions-ctl2.md#randomlong), [randomString](string-functions-ctl2.md#randomstring), [randomUUID](string-functions-ctl2.md#randomuuid), [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed), [addNoise](mathematical-functions-ctl2.md#addnoise)

#### today

```ctl
date today();
```

The `today()` function accepts no argument and returns current date and time.

**Compatibility**

The `today()` function is available since **CloverETL 3.0.0**.
Example 116. Usage of today The `today()` function returns, for example, `2013-11-06 12:32:15` provided today is 6 November 2013 and the time is 12:32:15.
**See also:**[zeroDate](date-functions-ctl2.md#zerodate)

#### zeroDate

```ctl
date zeroDate();
```

The `zeroDate()` function accepts no argument and returns 1.1.1970 0:00:00 GMT.

**Compatibility**

The `zeroDate()` function is available since **CloverETL 3.0.0**.

**See also:**[today](date-functions-ctl2.md#today)

#### trunc
> [!IMPORTANT]
> The function `trunc` is **deprecated**. It returns a value and modifies the argument at the same time.

```ctl
date trunc(date arg);
```

The `trunc()` function removes time from date.

The function takes one date argument and returns the date with the same year, month and day, but hour, minute, second and millisecond values are set to 0.

If the argument is `null`, the function fails with an error.

The function `trunc` modifies the input parameter.

**Compatibility**

The `trunc(date)` function is available since **CloverETL 3.0.0**.

**See also:**[extractDate](date-functions-ctl2.md#extractdate), [truncDate](date-functions-ctl2.md#truncdate)

#### truncDate
> [!IMPORTANT]
> The function `truncDate` is **deprecated**. It returns a value and modifies the argument at the same time.

```ctl
date truncDate(date arg);
```

The `truncDate()` function returns a date with the same hour, minute, second and millisecond as the given date, but year is 1970, month and day values are set to 1. The 0 date is 1970-01-01.

If the given argument is `null`, the function fails with an error.

The function `truncDate` modifies the input parameter.

**Compatibility**

The function `truncDate(date)` is available since **CloverETL 3.0.0**.

**See also:**[extractTime](date-functions-ctl2.md#extracttime), [trunc](date-functions-ctl2.md#trunc)
