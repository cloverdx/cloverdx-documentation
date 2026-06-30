<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Lookup table functions -->

### Lookup table functions

#### List of functions

| [count](lookup-table-functions-ctl2.md#count) |
| --- |
| [get](lookup-table-functions-ctl2.md#get) |
| [next](lookup-table-functions-ctl2.md#next) |
| [put](lookup-table-functions-ctl2.md#put) |

Lookup table functions serve for lookup and manipulation with lookup tables. (See [Lookup Tables](lookup-tables.md).) To use the lookup table function, you need to specify the name of the lookup table as an argument of the `lookup()` function.
> [!WARNING]
> Remember that you should not use the functions shown below in the `init()`, `preExecute()`, or `postExecute()` functions of CTL template.
> [!WARNING]
> It is not possible to have multiple queries to the same lookup table at the same time as there is only one state which holds the next record.

#### count

`lookup(<lookup name>).count(keyValue)`

The `count()` function returns the number of records whose key value equals to `keyValue`.

The `count()` function used with DB lookup tables may return -1 instead of real count of record with specified key value (if you do not set **Max cached size** to a non-zero value).

The `lookup name` is simply a name of the lookup table. It is **not** specified as a string enclosed with `"` character.

The `keyValue` is a value of a key of the lookup table. If the lookup table has a key of one field, `keyValue` is one string. If the lookup table has a key of more fields, `keyValue` is specified as series of the values of particular key parts.

See the documentation of the particular lookup table for handling of duplicated keys.

**Compatibility**

The `count(string)` function is available since **CloverETL 3.0.x**.
Example 333. Usage of count
A lookup table with a one-field key.

```ctl
$out.0.count = lookup(names).count("smithj");
```

A lookup table with a key of two fields.

```ctl
$out.0.count = lookup(names).count("John", "Smith");
```

**See also:**[get](lookup-table-functions-ctl2.md#get)[Allow key duplicates](lookup-tables.md#lookup-tables-allow-key-duplicates)

#### get

`lookup(<lookup name>).get(keyValue)[.<field name>|.*]`

The function `get` searches the first record whose key value is equal to the value specified in the `get(keyValue)` function.

It returns the record of the lookup table. You can map it to other records in CTL2 (with the same metadata). If you want to get the value of the field, you can add the `.<field name>` part to the expression or `.*` to get the values of all fields.

If there is no record with the requested `keyValue` in the lookup table, the function returns `null`.

The `keyVal` in the function is a sequence of values of the field names separated by comma (not semicolon!). The key has the following form: `keyValuePart1,keyValuePart2,…,keyValuePartN`.

**Compatibility**

The `get(string)` function is available since **CloverETL 3.2.2** or earlier.
Example 334. Usage of get
There is a lookup table `users` having fields `name`, `surname`, `phone`. The key is formed by fields `name` and `surname`.

The phone of `John Smith` is acquired by the statement:

```ctl
$out.0.phone = lookup(users).get("John", "Smith").phone;
```

You can get the whole record:

```ctl
UsersMetadata u = lookup(users).get("John", "Smith");
```

As the `get()` function returns `null` if no record is found, getting the whole records allows you to do better error handling.

```ctl
UsersMetadata u = lookup(users).get("John", "Smith");
if (u != null) {
    $out.0.phone = u.phone;
}
```

**See also:**[count](lookup-table-functions-ctl2.md#count), [next](lookup-table-functions-ctl2.md#next), [put](lookup-table-functions-ctl2.md#put)

#### next

`lookup(<lookup name>).next()[.<field name>|.*]`

The `next()` function allows you to iterate the result of the search. It moves the pointer to the next record and returns this record.

It returns the next record with the same key. If there is no such record, it returns `null`.

**Compatibility**

The `next()` function is available since **CloverETL 3.2.2** or earlier.
Example 335. Usage of next
The basic usage:

```ctl
Record tmp = lookup(users).next()
```

The `next()` function is generally used in combination with `get()` function:

```ctl
// Process all records from a lookup
User user = lookup(users).get($in.0.userId);

while (user != null) {
    // Do something with user

    // Grab next user
    user = lookup(users).next();
}
```

**See also:**[get](lookup-table-functions-ctl2.md#get), [isnull](miscellaneous-functions-ctl2.md#isnull)

#### put

`lookup(<lookup name>).put(<record>)`

The `put()` function stores the record passed as its argument in the selected lookup table.

It returns a boolean result indicating whether the operation has succeeded or not.

Note that the metadata of the passed record must match the metadata of the lookup table.

The operation may not be supported by all types of lookup tables (it is not supported by **Database lookup tables**, for example) and its exact semantics is implementation-specific (in particular, the stored records may not be immediately available for reading in the same phase).

**Compatibility**

The `put(record)` function is available since **CloverETL 3.4.x**.
Example 336. Usage of put

```ctl
//Users is a same record as in the lookup table
Users u;
u.name = "John";
u.surname = "Smith";
u.username = "smithj";
lookup(users).put(u);
```

**See also:**[get](lookup-table-functions-ctl2.md#get)
Example 337. Usage of Lookup Table Functions
A **UsersLookup** lookup table contains **Firstname**, **Surname**, and **Username** columns. **Firstname** and **Surname** fields form the key. Lookup all **Usernames** for each particular **Firstname** and **Surname** tuple received from an input port.

```ctl
//#CTL2

function integer transform() {
    string[] usernames;

    // getting the first record
    // whose key value equals to $in.0.Surname, $in.0.Firstname tuple
    UsersMetadata usersRecord = lookup(UsersLookup).get($in.0.Surname, $in.0.Firstname);

    // iterate through all records found
    while (!isnull(usersRecord)) {
        usernames = append(usernames, usersRecord.Username);

        // searching the next record with the key specified above
        usersRecord = lookup(UsersLookup).next();
    }

    // mapping to the output
    $out.0.Surname   = $in.0.Surname;
    $out.0.Firstname = $in.0.Firstname;
    $out.0.Username  = usernames;

    return ALL;
}
```

> [!IMPORTANT]
> Remember that DB lookup tables cannot be used in compiled mode. (code starts with the following header: `//#CTL2:COMPILE`)
>
> You need to switch to interpreted mode (with the header: `//#CTL2`) to be able to access DB lookup tables from CTL2.
