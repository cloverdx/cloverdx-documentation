<!-- Development > Component reference > Transformers > DataSampler -->

### DataSampler

![DataSampler 64x64](../figures/DataSampler-64x64.png)

| [Short description](datasampler.md#short-description) |
| --- |
| [Ports](datasampler.md#ports) |
| [DataSampler attributes](datasampler.md#datasampler-attributes) |
| [Details](datasampler.md#details) |
| [See also](datasampler.md#see-also) |

#### Short description

**DataSampler** passes only some input records to the output. There is a range of filtering strategies you can select from to control the transformation.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1-N | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any |
| Output | 0 | **✓** | For sampled data records | Input0 |

#### DataSampler attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Sampling method | yes | The filtering strategy that determines which records will be passed to the output. Individual strategies you can choose from are described in [Details](datasampler.md#details). | Simple\|Systematic\|Stratified\|PPS |
| Required sample size | yes | The desired size of output data expressed as a fraction of the input. If you want the output to be e.g. 15% (roughly) of the input size, set this attribute to 0.15. | (0; 1) |
| Sampling key | [[1]](datasampler.md#datasampler-footnote1) | A field name the **Sampling method** uses to define strata. Field names can be chained in a sequence separated by a colon, semicolon or pipe. Every field can be followed by an order indicator in brackets (**a** for ascending, **d** for descending, **i** for ignore and **r** for automatic estimate). For description of indicator meaning, see [Ordering type](components.md#ordering-type). | e.g. Surname(a); FirstName(i); Salary(d) |
| Advanced |  |  |  |
| Random seed |  | A `long` number that is used in the random generator. It assures that results are random but remain identical on every graph run. | <0; N> |

| 1 |  |
| --- | --- |

 The attribute is required in all sampling methods except for **Simple**.

#### Details

**DataSampler** receives data on its single input edge. It then filters input records and passes only some of them to the output. You can control which input records are passed by selecting one of the filtering strategies called **Sampling methods**. The input and output metadata have to match each other.

A typical use case for **DataSamper** can be imagined like this. You want to check whether your data transformation works properly. In case you are processing millions of records, it might be useful to get only a few thousands and observe. Using this component, you can create such data sample.

**DataSampler** offers four **Sampling methods** to create a representative sample of the whole data set:

- **Simple** - every record has an equal chance of being selected. The filtering is based on a `double` value chosen (approximately uniformly) from the <0.0d; 1.0d) interval. A record is selected if the drawn number is lower than **Required sample size**.
- **Systematic** - has a random start. It then proceeds by selecting every k-th element of the ordered list. The first element and interval derive from **Required sample size**. The method depends on the data set being arranged in a sort order given by **Sampling key** (for the results to be representative).
  There are also cases when you might need to sample an unsorted input. Even though you always have to specify **Sampling key**, remember you can suppress its sort order by setting the order indicator to **i** for "ignore". This ensures the data set’s sort order will not be regarded. Example key setting: "InvoiceNumber(i)".
- **Stratified** - if the data set contains a number of distinct categories, the set can be organized by these categories into separate *strata*. Each *stratum* is then sampled as an independent sub-population out of which individual elements are selected on a random basis. At least one record from each stratum is selected. The record is compared with previous one whether or not it is in the same stratum. If the input is unsorted, stratum may be split into several parts and processed in the same way as more strata.
- **PPS** (Probability Proportional to Size Sampling) - probability for each record is set to proportional to its *stratum* size up to a maximum of 1. Strata are defined by the value of the field you have chosen in **Sampling key**. The method then uses **Systematic** sampling for each group of records.

Comparing the methods, **Simple** random sampling is the simplest and quickest one. It suffices in most cases. **Systematic** sampling with no sorting order is as fast as **Simple** and produces a strongly representative data probe, too. **Stratified** sampling is the trickiest one. It is useful only if the data set can be split into separate groups of reasonable sizes. Otherwise the data probe is much bigger than requested. For a deeper insight into sampling methods in statistics, see [Wikipedia](http://en.wikipedia.org/wiki/Sampling_%28statistics%29#Sampling_methods).

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Transformers comparison](common-of-transformers.md#transformers-comparison) |
