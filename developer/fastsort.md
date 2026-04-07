<!-- Development > Component reference > Transformers > FastSort -->

### FastSort

![FastSort 64x64](../figures/FastSort-64x64.png)

| [Short description](fastsort.md#short-description) |
| --- |
| [Ports](fastsort.md#ports) |
| [Metadata](fastsort.md#metadata) |
| [FastSort attributes](fastsort.md#fastsort-attributes) |
| [Details](fastsort.md#details) |
| [Best practices](fastsort.md#best-practices) |
| [Compatibility](fastsort.md#compatibility) |
| [See also](fastsort.md#see-also) |

#### Short description

**FastSort** sorts input records using a sort key. **FastSort** is faster than **ExtSort**, but requires more system resources and sorting is not stable.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1-N | - | - | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records. | The same input and output metadata. |
| Output | 0 | **✓** | For sorted data records. |  |
| 1-N | **⨯** | For sorted data records. |  |  |

#### Metadata

Metadata can be propagated through this component. All output metadata must be the same.

#### FastSort attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Sort key | **✓** | A list of fields (separated by a semicolon) according to which the data records are sorted, including a sorting order for each data field separately, see [Sort key](components.md#sort-key). |  |
| In memory only |  | If `true`, internal sorting is forced and all attributes except **Sort key** and **Run size** are ignored. | false (default) \| true |
| Advanced |  |  |  |
| Run size (records) |  | The number of records sorted at once in memory; the size of one read buffer. Largely affects speed and memory requirements, see [Run Size](fastsort.md#run-size). Multiplies with **Number of read buffers** (which depends on the **Number of sorting threads**).  Reasonable **Run size**s vary from 5,000 to 200,000 based on the record size and the total number of records. | 10000 (default) \| 1000 - N |
| Max open files |  | Limits the number of temp files that can be created during the sorting. Too low number (500 or less) significantly reduces performance, see [Max open files](fastsort.md#max-open-files). 0 denotes that the number of temp files is unlimited. | 1000 (default) \| 1-N \| 0 (unlimited) |
| Number of sorting threads |  | The number of worker threads to do the job. Setting this value too high may even slow the graph run down, see [Number of sorting threads](fastsort.md#number-of-sorting-threads). Also affects memory requirements. | 1 (default) \| 1-N |
| Number of read buffers |  | How many chunks of data (each the size of **Run size**) will be held in memory at a time, see [Number of read buffers](fastsort.md#number-of-read-buffers). Defaults to **Number of sorting threads** + 2. | auto (default) \| 1-N |
| Tape buffer size (bytes) |  | A buffer used by a worker for filling the output. Slightly affects performance, see [Tape buffer size](fastsort.md#tape-buffer-size). | 8192 (default) \| 1-N |
| Compress temporary files |  | If `true`, temporary files are compressed. For more information, see [Compress temporary files](fastsort.md#compress-temporary-files). | false (default) \| true |
| Deprecated |  |  |  |
| Estimated record count | [[1]](fastsort.md#records-fastsort) | An estimated number of input records to be sorted. | auto (default) \| 1-N |
| Average record size (bytes) | [[2]](fastsort.md#runsize-fastsort) | Guess on average byte size of records. | auto (default) \| 1-N |
| Maximum memory (MB, GB) | [[2]](fastsort.md#runsize-fastsort) | Rough estimate of maximum memory that can be used. | auto (default) \| 1-N |
| Sorting locale |  | Locale used for a correct sorting order. | none (default) \| any locale |
| Case sensitive |  | By default (**Sorting locale** is `none`), upper-case characters are sorted separately and precede lower-case characters that are sorted separately, too. If **Sorting locale** is set, upper- and lower-case characters are sorted together; if **Case sensitive** is `true`, a lower-case precedes corresponding upper-case, while `false` preserves the order in which data strings appear in the input.  A case sensitive attribute value is taken into account only if **Locale** is set. | false (default) \| true |

| 1 |  |
| --- | --- |

 **Estimated record count** is a helper attribute which is used for calculating (rather unnatural) **Run size** automatically as approximately **Estimated record count** to the power 0.66. If **Run size** is set explicitly, **Estimated record count** is ignored.

| 2 |  |
| --- | --- |

 These attributes affect automatic guess of **Run size**. Generally, the following formula must be true:

**Number of read buffers** * **Run size** * **Average record size** < **Maximum memory**

#### Details

**FastSort** is a high performance sort component reaching the optimal efficiency when enough system resources are available. **FastSort** can be up to 2.5 times faster than **ExtSort**, but consumes significantly more memory and temporary disk space.

The component takes input records and sorts them using a sorting key - a single field or a set of fields. You can specify sorting order for each field in the key separately. The sorted output is sent to all connected ports.

Satisfactory results can be obtained with default settings (just the sorting key must be specified). However, to achieve the best performance, a number of parameters is available for tweaking.
> [!WARNING]
> **FastSort** does not preserve order of records with equal key value (sorting algorithm is not [stable](http://en.wikipedia.org/wiki/Sorting_algorithm#Stability)). If stability is required, please use [ExtSort](extsort.md) instead.

##### Sorting null values

In ascending order, null values are sorted before strings, numbers, booleans, or dates. If you sort data in descending order, null values are sorted after strings, numbers, booleans, or dates.

Remember that **FastSort** processes the records in which the same fields of the **Sort key** attribute have `null` values as if these `nulls` were equal.

##### FastSort tweaking

Basically, you do not need to set any of these attributes; however, sometimes you can increase performance by setting them. You may have limited memory or you need to sort a large number of records, or these records are too big. In similar cases, you can adjust **FastSort** to your needs.
> [!TIP]
> The memory requirements of the component can be estimated as follows:
>
> - heap memory = **Number of read buffers** × **Run size** × estimated record size
> - direct memory = **Max open files** × **Tape buffer size**

###### Run size

The core attribute for **FastSort**. Determines how many records form a "run" (i.e. a group of sorted records in temp files). The lower **Run size**, the more temp files get created, less memory is used and greater speed is achieved. On the other hand, higher values might cause memory issues. There is no rule of thumb as to whether **Run size** should be high or low to get the best performance. Generally, the more records you are about to sort, the bigger **Run size** you might want. The rough formula for **Run size** is **Estimated record count**^0.66. Note that memory consumption multiplies with **Number of read buffers**, which in turn grows with **Number of sorting threads**. So, higher **Run size**s result in much higher memory footprints.

###### Max open files

**FastSort** uses relatively large numbers of temporary files during its operation. By default, the number of temporary files is limited to 1,000. For production systems, it is recommended to set the limit as high as possible, because there is no speed sacrifice, see [Performance bottlenecks](fastsort.md#performance-bottlenecks). On the other hand, you can lower the limit even further to prevent hitting the user quota or other OS-specific limits and runtime limitations. The following table should give you a better idea:

| Dataset size | Number of temp. files | Default Run size | Note |
| --- | --- | --- | --- |
| 1,000,000 | ~100 | ~10,000 |  |
| 10,000,000 | ~250 | ~45,000 |  |
| 1,000,000,000 | 20,000 to 2,000 | 50,000 to 500,000 | Depends on available memory |

Note that numbers in the table above are not exact and might be different on your system.

###### Number of sorting threads

Tells **FastSort** how many runs (chunks) should be sorted at a time in parallel. By default, it is automatically set to 1 or 2 based on the number of CPU cores in your system. Overriding this value makes sense if your system has lots of CPU cores and your disk performance can handle working with so many parallel data streams.

###### Number of read buffers

This setting corresponds tightly to **Number of sorting threads** - must be equal to or greater than **Number of sorting threads**. The higher the number of read buffers, the lower chance the workers will block each other. Defaults to **Number of sorting threads** + 2.

###### Compress temporary files

Along with **Temporary files charset**, this option lets you reduce the space required for temporary files. Note that compression can save a lot of space but **decreases the performance by up to 30%**.

###### Tape buffer size

Size (in bytes) of a file output buffer. The default value is 8kB. Decreasing this value might avoid memory exhaustion for large numbers of runs (e.g. when **Run size** is very small compared to the total number of records). However, the impact of this setting is quite small.

#### Best practices

Make sure you have dedicated enough memory to your Java Virtual Machine (JVM). Having plenty of memory available, **FastSort** is capable of doing astonishing job. Remember that the default JVM heap space (64MB) can cause **FastSort** to crash. For best results, try to increase the memory value up to 2GB (if possible, while still leaving enough memory for the operating system). How to set the JVM is described in [Runtime configuration](../admin/designer-configuration.md#runtime-configuration).

##### Performance bottlenecks

- *Sorting big records (long string fields, tens or hundreds of fields, etc.):***FastSort** is greedy for both memory and CPU cores. If the system does not have enough of either, **FastSort** can easily crash with the `out-of-memory` error. In such a case, use the **ExtSort** component instead.
- *Utilizing more than 2 CPU cores:* Unless you are using very fast disk drives, overriding the default value of **Number of sorting threads** to more than 2 threads does not necessarily help. It can even slightly slow the process down, as extra memory is loaded for each additional thread.
- *Coping with quotas and other runtime limitations:* In complex graphs with several parallel sorts, even with other graph components also having huge number of open files, the `Too many open files` error and graph execution failure may occur. There are two possible solutions to this issue:
  1. increase the limit (quota) This option is recommended for production systems since there is no speed sacrifice. Typically, setting limit to higher number on Unix systems.
  2. force **FastSort** to keep the number of temporary files below some limit For regular users on large servers, increasing the quota is not an option. Thus, **Max open files** must be set to a reasonable value. **FastSort** then performs intermediate merges of temporary files to keep their number below the limit. However, setting **Max open files** to values, for which such merges are inevitable, often produces significant performance drop. So keep it at the highest possible value. If you are forced to limit **FastSort** to less than a hundred temporary files, even for large datasets, consider using **ExtSort** instead which is designed for performance with a limited number of tapes.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 2.2.0 | **FastSort** is available since **2.2.0**. |

#### See also

| [ExtSort](extsort.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Transformers comparison](common-of-transformers.md#transformers-comparison) |
