<!-- Development > Component reference > Job Control > ExecuteMapReduce -->

### ExecuteMapReduce

Jobflow Component

![ExecuteMapReduce 64x64](../figures/ExecuteMapReduce-64x64.png)

| [Short description](executemapreduce.md#short-description) |
| --- |
| [Ports](executemapreduce.md#ports) |
| [Metadata](executemapreduce.md#metadata) |
| [ExecuteMapReduce attributes](executemapreduce.md#executemapreduce-attributes) |
| [Details](executemapreduce.md#details) |
| [See also](executemapreduce.md#see-also) |

#### Short description

**ExecuteMapReduce** runs specified MapReduce job on a Hadoop cluster.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **⨯** | **⨯** | 0-1 | 0-2 | **⨯** | **⨯** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | Input tokens with MapReduce job execution settings. | Any |
| Output | 0 | **⨯** | Execution information for successful jobs. | Any |
| 1 | **⨯** | Execution information for unsuccessful jobs. | Any |  |

#### Metadata

This component has metadata templates available. See details on [metadata templates](components.md#metadata-templates).

#### ExecuteMapReduce attributes

| Attribute | Req | Description | Possible values |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Basic |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Hadoop connection | yes | [Hadoop connections](hadoop-connections.md) which defines both connection to HDFS server (NameNode) and connection to MapReduce server (JobTracker). |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job name | no | An arbitrary label of a job execution. The default value is the name of a specified MapReduce `.jar` file. | Any string |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| An URL of a JAR file with job classes | yes | The path to a `.jar` file with MapReduce job. The file has to be on a local file system. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Timeout (ms) | no | Time limit for a job execution in milliseconds. If the job execution time exceeds this limit, the job is killed. Set to 0 (default) for no limit. | 0 (unlimited) \| positive number |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Input mapping | no | Input mapping defines how data from an incoming token overrides default execution settings. | CTL transformation |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Output mapping | no | Output mapping maps results of successful MapReduce jobs to the first output port. See [Output and error mappings](executemapreduce.md#output-and-error-mappings). | CTL transformation |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Error mapping | no | Error mapping maps results of unsuccessful jobs to the second output port. See [Output and error mappings](executemapreduce.md#output-and-error-mappings). | CTL transformation |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Redirect error output | no | By default, results of failed jobs are sent to the second output port (error port). If this switch is set to `true`, results of unsuccessful jobs are sent to the first output port in the same way as successful jobs. | `false` (default) \| `true` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job folders |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Input files | yes | One or more paths to input files located on HDFS. The path can be specified in a form of HDFS URL, e.g. `hdfs://CONN_ID/path/to/inputfile`, where the Hadoop connection ID `CONN_ID` has to match the ID of the connection specified in the **Hadoop connection** attribute, or it can be simply a path on the HDFS, either absolute, e.g. `/path/to/inputfile`, or relative to job’s working directory, e.g. `relative/path/to/inputfile`. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Output directory | yes | The path to an output directory located on HDFS. The directory will be created if it does not already exist (see the **Clear output directory before execution** attribute). An HDFS URL or absolute/working-directory-relative path on HDFS can be specified here, just as in the **Input files** attribute, e.g. `hdfs://CONN_ID/path/to/outputdir`, `/path/to/outputdir` or `relative/path/to/outputdir`. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Working directory | no | A location of the working directory of MapReduce job on HDFS. This can be an HDFS URL, e.g. `hdfs://CONN_ID/path/to/workdir`, or an absolute path on the HDFS, e.g. `/path/to/workdir`. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Clear output directory before execution | no | Indicates whether the **Output directory** should be deleted before starting the job. If this is set to `false` and the output directory already exists before job execution, the job will fail to start and an error appears stating that the output directory already exists. | `false` (default) \| `true` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Classes |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job implementation API version | yes | A version of an API used to implement the MapReduce job. If **New API** is selected (default), classes implementing the job have to extend classes from the `org.apache.hadoop.mapreduce` package. If **Old API** is selected, classes implementing the job extend/implement classes/interfaces from the `org.apache.hadoop.mapred` package. | `mapreduce` (default) \| `mapred` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Mapper class | no | A fully qualified name of a Java class to be used as a mapper of the job. Definition of the class is typically found in the job JAR file.  Depending on the selected **Job implementation API version**, the class must extend/implement class/interface from the following table:  \| Extends/implements \|  \| \| --- \| --- \| \| New API \| `org.apache.hadoop.mapreduce.Mapper` \| \| Old API \| `org.apache.hadoop.mapred.Mapper` \|  The following table contains a job configuration parameter and Hadoop API method which correspond to setting this component attribute. The **ExecuteMapReduce** component always directly sets the job configuration parameter according to selected **Job implementation API version** (listed Java methods are never called and are listed just for comparison).  \| Job configuration \|  \|  \| \| --- \| --- \| --- \| \| Parameter \| New API \| `mapreduce.map.class` \| \| Old API \| `mapred.mapper.class` \|  \| \| Method \| New API \| `Job.setMapperClass(Class)` \| \| Old API \| `JobConf.setMapperClass(Class)` \|  \| | Extends/implements |  | New API | `org.apache.hadoop.mapreduce.Mapper` | Old API | `org.apache.hadoop.mapred.Mapper` | Job configuration |  |  | Parameter | New API | `mapreduce.map.class` | Old API | `mapred.mapper.class` | Method | New API | `Job.setMapperClass(Class)` | Old API | `JobConf.setMapperClass(Class)` | A fully qualified class name, e.g. `com.acme.MyMap`  \| Default \|  \| \| --- \| --- \| \| New API \| `org.apache.hadoop.mapreduce.Mapper` \| \| Old API \| `org.apache.hadoop.mapred.lib.IdentityReducer` \| | Default |  | New API | `org.apache.hadoop.mapreduce.Mapper` | Old API | `org.apache.hadoop.mapred.lib.IdentityReducer` |
| Extends/implements |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| New API | `org.apache.hadoop.mapreduce.Mapper` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `org.apache.hadoop.mapred.Mapper` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job configuration |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Parameter | New API | `mapreduce.map.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `mapred.mapper.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Method | New API | `Job.setMapperClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `JobConf.setMapperClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Default |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| New API | `org.apache.hadoop.mapreduce.Mapper` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `org.apache.hadoop.mapred.lib.IdentityReducer` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Combiner class | no | A fully qualified name of a Java class to be used as a combiner of the job. The definition of the class is typically found in the job JAR file.  \| Extends/implements \|  \| \| --- \| --- \| \| New API \| `org.apache.hadoop.mapreduce.Reducer` \| \| Old API \| `org.apache.hadoop.mapred.Reducer` \|  \| Job configuration \|  \|  \| \| --- \| --- \| --- \| \| Parameter \| New API \| `mapreduce.combine.class` \| \| Old API \| `mapred.combiner.class` \|  \| \| Method \| New API \| `Job.setCombinerClass(Class)` \| \| Old API \| `JobConf.setCombinerClass(Class)` \|  \| | Extends/implements |  | New API | `org.apache.hadoop.mapreduce.Reducer` | Old API | `org.apache.hadoop.mapred.Reducer` | Job configuration |  |  | Parameter | New API | `mapreduce.combine.class` | Old API | `mapred.combiner.class` | Method | New API | `Job.setCombinerClass(Class)` | Old API | `JobConf.setCombinerClass(Class)` | A fully qualified class name, e.g. `com.acme.MyReduce` \| No combiner (default) |  |  |  |  |  |  |
| Extends/implements |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| New API | `org.apache.hadoop.mapreduce.Reducer` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `org.apache.hadoop.mapred.Reducer` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job configuration |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Parameter | New API | `mapreduce.combine.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `mapred.combiner.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Method | New API | `Job.setCombinerClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `JobConf.setCombinerClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Partitioner class | no | A fully qualified name of a Java class to be used as a partitioner of the job. The definition of the class is typically found in the job JAR file.  \| Extends/implements \|  \| \| --- \| --- \| \| New API \| `org.apache.hadoop.mapreduce.Partitioner` \| \| Old API \| `org.apache.hadoop.mapred.Partitioner` \|  \| Job configuration \|  \|  \| \| --- \| --- \| --- \| \| Parameter \| New API \| `mapreduce.partitioner.class` \| \| Old API \| `mapred.partitioner.class` \|  \| \| Method \| New API \| `Job.setPartitionerClass(Class)` \| \| Old API \| `JobConf.setPartitionerClass(Class)` \|  \| | Extends/implements |  | New API | `org.apache.hadoop.mapreduce.Partitioner` | Old API | `org.apache.hadoop.mapred.Partitioner` | Job configuration |  |  | Parameter | New API | `mapreduce.partitioner.class` | Old API | `mapred.partitioner.class` | Method | New API | `Job.setPartitionerClass(Class)` | Old API | `JobConf.setPartitionerClass(Class)` | A fully qualified class name, e.g. `com.acme.MyPartitioner`  \| Default \|  \| \| --- \| --- \| \| New API \| `org.apache.hadoop.mapreduce.lib.partition.HashPartitioner` \| \| Old API \| `org.apache.hadoop.mapred.lib.HashPartitioner` \| | Default |  | New API | `org.apache.hadoop.mapreduce.lib.partition.HashPartitioner` | Old API | `org.apache.hadoop.mapred.lib.HashPartitioner` |
| Extends/implements |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| New API | `org.apache.hadoop.mapreduce.Partitioner` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `org.apache.hadoop.mapred.Partitioner` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job configuration |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Parameter | New API | `mapreduce.partitioner.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `mapred.partitioner.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Method | New API | `Job.setPartitionerClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `JobConf.setPartitionerClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Default |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| New API | `org.apache.hadoop.mapreduce.lib.partition.HashPartitioner` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `org.apache.hadoop.mapred.lib.HashPartitioner` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Reducer class | no | A fully qualified name of a Java class to be used as a reducer of the job. The definition of the class is typically found in the job JAR file.  \| Extends/implements \|  \| \| --- \| --- \| \| New API \| `org.apache.hadoop.mapreduce.Reducer` \| \| Old API \| `org.apache.hadoop.mapred.Reducer` \|  \| Job configuration \|  \|  \| \| --- \| --- \| --- \| \| Parameter \| New API \| `mapreduce.reduce.class` \| \| Old API \| `mapred.reducer.class` \|  \| \| Method \| New API \| `Job.setReducerClass(Class)` \| \| Old API \| `JobConf.setReducerClass(Class)` \|  \| | Extends/implements |  | New API | `org.apache.hadoop.mapreduce.Reducer` | Old API | `org.apache.hadoop.mapred.Reducer` | Job configuration |  |  | Parameter | New API | `mapreduce.reduce.class` | Old API | `mapred.reducer.class` | Method | New API | `Job.setReducerClass(Class)` | Old API | `JobConf.setReducerClass(Class)` | A fully qualified class name, e.g. `com.acme.MyReduce`  \| Default \|  \| \| --- \| --- \| \| New API \| `org.apache.hadoop.mapreduce.Reducer` \| \| Old API \| `org.apache.hadoop.mapred.lib.IdentityReducer` \| | Default |  | New API | `org.apache.hadoop.mapreduce.Reducer` | Old API | `org.apache.hadoop.mapred.lib.IdentityReducer` |
| Extends/implements |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| New API | `org.apache.hadoop.mapreduce.Reducer` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `org.apache.hadoop.mapred.Reducer` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job configuration |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Parameter | New API | `mapreduce.reduce.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `mapred.reducer.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Method | New API | `Job.setReducerClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `JobConf.setReducerClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Default |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| New API | `org.apache.hadoop.mapreduce.Reducer` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `org.apache.hadoop.mapred.lib.IdentityReducer` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Mapper output key class | no | A fully qualified name of a Java class whose instances are the keys of mapper output records. Has to be specified only if the mapper output key class is different than the final output value class.  \| Job configuration \|  \|  \| \| --- \| --- \| --- \| \| Parameter \| `mapred.mapoutput.key.class` \|  \| \| Method \| New API \| `Job.setMapOutputKeyClass(Class)` \| \| Old API \| `JobConf.setMapOutputKeyClass(Class)` \|  \| | Job configuration |  |  | Parameter | `mapred.mapoutput.key.class` |  | Method | New API | `Job.setMapOutputKeyClass(Class)` | Old API | `JobConf.setMapOutputKeyClass(Class)` | A fully qualified class name, e.g. `org.apache.hadoop.io.Text` \| Default is the value of the **Output key class** attribute |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job configuration |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Parameter | `mapred.mapoutput.key.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Method | New API | `Job.setMapOutputKeyClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `JobConf.setMapOutputKeyClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Mapper output value class | no | A fully qualified name of a Java class whose instances are the values of mapper output records. Has to be specified only if the mapper output value class is different than the final output value class.  \| Job configuration \|  \|  \| \| --- \| --- \| --- \| \| Parameter \| `mapred.mapoutput.value.class` \|  \| \| Method \| New API \| `Job.setMapOutputValueClass(Class)` \| \| Old API \| `JobConf.setMapOutputValueClass(Class)` \|  \| | Job configuration |  |  | Parameter | `mapred.mapoutput.value.class` |  | Method | New API | `Job.setMapOutputValueClass(Class)` | Old API | `JobConf.setMapOutputValueClass(Class)` | A fully qualified class name, e.g. `org.apache.hadoop.io.Text` \| Default is the value of the **Output value class** attribute |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job configuration |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Parameter | `mapred.mapoutput.value.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Method | New API | `Job.setMapOutputValueClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `JobConf.setMapOutputValueClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Grouping comparator | no | A fully qualified name of a Java class implementing a comparator that decides which keys are grouped together for a single call to the `reduce` method of the reducer. The class has to implement the `org.apache.hadoop.io.RawComparator` interface (or extend its base implementation `org.apache.hadoop.io.WritableComparator`).  \| Job configuration \|  \|  \| \| --- \| --- \| --- \| \| Parameter \| `mapred.output.value.groupfn.class` \|  \| \| Method \| New API \| `Job.setGroupingComparatorClass(Class)` \| \| Old API \| `JobConf.setOutputValueGroupingComparator(Class)` \|  \| | Job configuration |  |  | Parameter | `mapred.output.value.groupfn.class` |  | Method | New API | `Job.setGroupingComparatorClass(Class)` | Old API | `JobConf.setOutputValueGroupingComparator(Class)` | A fully qualified class name, e.g. `com.acme.MyGroupingComp` \| The default class is derived in these steps: 1) take the class name value of the **Sorting comparator** attribute, if specified; otherwise 2) take implementation of `org.apache.hadoop.io.WritableComparable` registered as the comparator for the **Mapper output key class**, if registered; otherwise 3) take the generic implementation, i.e. `org.apache.hadoop.io.WritableComparator`. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job configuration |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Parameter | `mapred.output.value.groupfn.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Method | New API | `Job.setGroupingComparatorClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `JobConf.setOutputValueGroupingComparator(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Sorting comparator | no | A fully qualified name of a Java class implementing a comparator that controls how the keys are sorted before they are passed to the reducer. The class has to implement the `org.apache.hadoop.io.RawComparator` interface (or extend its base implementation `org.apache.hadoop.io.WritableComparator`).  \| Job configuration \|  \|  \| \| --- \| --- \| --- \| \| Parameter \| `mapred.output.key.comparator.class` \|  \| \| Method \| New API \| `Job.setSortComparatorClass(Class)` \| \| Old API \| `JobConf.setOutputKeyComparatorClass(Class)` \|  \| | Job configuration |  |  | Parameter | `mapred.output.key.comparator.class` |  | Method | New API | `Job.setSortComparatorClass(Class)` | Old API | `JobConf.setOutputKeyComparatorClass(Class)` | A fully qualified class name, e.g. `com.acme.MySorter` \| The default class is the implementation of `org.apache.hadoop.io.WritableComparable` registered as a comparator for the **Mapper output key class**, if registered; otherwise the generic implementation `org.apache.hadoop.io.WritableComparator` is used. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job configuration |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Parameter | `mapred.output.key.comparator.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Method | New API | `Job.setSortComparatorClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `JobConf.setOutputKeyComparatorClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Output key class | yes | A fully qualified name of a Java class whose instances are keys of output records of the job (i.e. output of the reducer).  \| Job configuration \|  \|  \| \| --- \| --- \| --- \| \| Parameter \| `mapred.output.key.class` \|  \| \| Method \| New API \| `Job.setOutputKeyClass(Class)` \| \| Old API \| `JobConf.setOutputKeyClass(Class)` \|  \| | Job configuration |  |  | Parameter | `mapred.output.key.class` |  | Method | New API | `Job.setOutputKeyClass(Class)` | Old API | `JobConf.setOutputKeyClass(Class)` | A fully qualified class name, e.g. `org.apache.hadoop.io.Text` \| `org.apache.hadoop.io.LongWritable` (default) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job configuration |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Parameter | `mapred.output.key.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Method | New API | `Job.setOutputKeyClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `JobConf.setOutputKeyClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Output value class | yes | A fully qualified name of a Java class whose instances are values of output records of the job (i.e. output of the reducer).  \| Job configuration \|  \|  \| \| --- \| --- \| --- \| \| Parameter \| `mapred.output.value.class` \|  \| \| Method \| New API \| `Job.setOutputValueClass(Class)` \| \| Old API \| `JobConf.setOutputValueClass(Class)` \|  \| | Job configuration |  |  | Parameter | `mapred.output.value.class` |  | Method | New API | `Job.setOutputValueClass(Class)` | Old API | `JobConf.setOutputValueClass(Class)` | A fully qualified class name, e.g. `org.apache.hadoop.io.IntWritable` \| `org.apache.hadoop.io.Text` (default) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job configuration |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Parameter | `mapred.output.value.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Method | New API | `Job.setOutputValueClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `JobConf.setOutputValueClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Input format | no | A fully qualified name of a Java class that is to be used as an input format of the job. This class implements parsing of input files and produces key-value pairs which will serve as the input of the mapper.  \| Extends/implements \|  \| \| --- \| --- \| \| New API \| `org.apache.hadoop.mapreduce.InputFormat` \| \| Old API \| `org.apache.hadoop.mapred.InputFormat` \|  \| Job configuration \|  \|  \| \| --- \| --- \| --- \| \| Parameter \| New API \| `mapreduce.inputformat.class` \| \| Old API \| `mapred.input.format.class` \|  \| \| Method \| New API \| `Job.setInputFormatClass(Class)` \| \| Old API \| `JobConf.setInputFormat(Class)` \|  \| | Extends/implements |  | New API | `org.apache.hadoop.mapreduce.InputFormat` | Old API | `org.apache.hadoop.mapred.InputFormat` | Job configuration |  |  | Parameter | New API | `mapreduce.inputformat.class` | Old API | `mapred.input.format.class` | Method | New API | `Job.setInputFormatClass(Class)` | Old API | `JobConf.setInputFormat(Class)` | A fully qualified class name  \| Default \|  \| \| --- \| --- \| \| New API \| `org.apache.hadoop.mapreduce.lib.input.TextInputFormat` \| \| Old API \| `org.apache.hadoop.mapred.TextInputFormat` \| | Default |  | New API | `org.apache.hadoop.mapreduce.lib.input.TextInputFormat` | Old API | `org.apache.hadoop.mapred.TextInputFormat` |
| Extends/implements |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| New API | `org.apache.hadoop.mapreduce.InputFormat` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `org.apache.hadoop.mapred.InputFormat` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job configuration |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Parameter | New API | `mapreduce.inputformat.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `mapred.input.format.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Method | New API | `Job.setInputFormatClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `JobConf.setInputFormat(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Default |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| New API | `org.apache.hadoop.mapreduce.lib.input.TextInputFormat` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `org.apache.hadoop.mapred.TextInputFormat` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Output format | no | A fully qualified name of a Java class that is to be used as an output format of the job. This class implementation takes key-value pairs produced by the reducer and writes them into an output file.  \| Extends/implements \|  \| \| --- \| --- \| \| New API \| `org.apache.hadoop.mapreduce.OutputFormat` \| \| Old API \| `org.apache.hadoop.mapred.OutputFormat` \|  \| Job configuration \|  \|  \| \| --- \| --- \| --- \| \| Parameter \| New API \| `mapreduce.outputformat.class` \| \| Old API \| `mapred.output.format.class` \|  \| \| Method \| New API \| `Job.setOutputFormatClass(Class)` \| \| Old API \| `JobConf.setOutputFormat(Class)` \|  \| | Extends/implements |  | New API | `org.apache.hadoop.mapreduce.OutputFormat` | Old API | `org.apache.hadoop.mapred.OutputFormat` | Job configuration |  |  | Parameter | New API | `mapreduce.outputformat.class` | Old API | `mapred.output.format.class` | Method | New API | `Job.setOutputFormatClass(Class)` | Old API | `JobConf.setOutputFormat(Class)` | A fully qualified class name, e.g. `org.apache.hadoop.mapreduce.lib.output.SequenceFileOutputFormat` in which case, output files can be read using the [HadoopReader](hadoopreader.md) component.  \| Default \|  \| \| --- \| --- \| \| New API \| `org.apache.hadoop.mapreduce.lib.input.TextOutputFormat` \| \| Old API \| `org.apache.hadoop.mapred.TextOutputFormat` \| | Default |  | New API | `org.apache.hadoop.mapreduce.lib.input.TextOutputFormat` | Old API | `org.apache.hadoop.mapred.TextOutputFormat` |
| Extends/implements |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| New API | `org.apache.hadoop.mapreduce.OutputFormat` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `org.apache.hadoop.mapred.OutputFormat` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Job configuration |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Parameter | New API | `mapreduce.outputformat.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `mapred.output.format.class` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Method | New API | `Job.setOutputFormatClass(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `JobConf.setOutputFormat(Class)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Default |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| New API | `org.apache.hadoop.mapreduce.lib.input.TextOutputFormat` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Old API | `org.apache.hadoop.mapred.TextOutputFormat` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Advanced |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Number of mappers | no | A number of mapper tasks that should be run by Hadoop to execute the job. This is only a hint, the actual number of spawned map tasks depends on the input format class implementation. | Integer grater than zero |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Number of reducers | no | A number of required reducer tasks to be run by Hadoop to execute the job. It is legal to specify zero number of reducers in which case no reducer is run and the output of mappers goes directly to the **Output directory**. | Integer greater or equal to zero |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Execute job as daemon | no | By default, it is set to `false` and the **ExecuteMapReduce** component executes MapReduce jobs synchronously, i.e. it starts the job and waits until the job finishes, then it starts another job defined by the next input token (or finishes, if there are no more jobs to run).  If set to `true`, jobs are executed asynchronously, i.e. the component starts the job and, without waiting, immediately runs another job defined by the next input token (or finishes, if there are no more jobs to run). This also means that job runs are not monitored (no job run status is printed to the graph run log). | `false` (default) \| `true` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Stop processing on fail | no | By default, any failed MapReduce job causes the component to stop executing other jobs and information about skipped tokens is sent to the error output port. This behavior can be disabled by this attribute. **Note:** this function works only if an edge is connected to the component’s error port. | `true` (default) \| `false` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Additional job settings | no | Other properties of the job that need to be set can be specified here as key-value pairs. The key is a Hadoop specific name of the property (must be valid for the used version of Hadoop) and the value is a new value of the named property. Component attributes values have a higher priority than values of corresponding properties specified here.  Value of this field has to be in form of Java properties files.  For each executed job, an overview of all job settings (job.xml file) can be viewed on the JobTracker HTML status page (by default running on port 50030). |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
> [!NOTE]
> All of the component’s attributes described above can be also configured using data from input tokens. The **Input mapping** CTL transformation defines mapping from input token data fields to MapReduce job run configuration.
> [!TIP]
> When the **ExecutemapReduce** component creates job configuration, information about setting each parameter is printed with a **DEBUG** log level into the graph run log. Moreover, a complete final job configuration XML is printed with a **TRACE** log level.

#### Details

| [Output and error mappings](executemapreduce.md#output-and-error-mappings) |
| --- |

The **ExecuteMapReduce** component runs a Hadoop MapReduce job implemented using specified classes in a provided `.jar` file. The component periodically queries the Hadoop cluster for a job run status and prints this information to the graph log.

The MapReduce job classes can be implemented using both the new and old Hadoop MapReduce job API. Implementation using the new API means that job classes extend adequate classes from the `org.apache.hadoop.mapreduce` package, whereas job classes using the old API implement appropriate interfaces from the `org.apache.hadoop.mapred` package. By default, the `ExecuteMapReduce` component expects the new job API. If your job is implemented with the old API, you have to explicitly set the **Job implementation API version** attribute (see below).

As a typical **Job Control** component, **ExecuteMapReduce** can have a single input port and two output ports attached. The component reads an input token, executes a MapReduce job based on incoming data values, waits for the job to finish, and sends the results of a successful job to the first output port and the results of a failed job to the second output port (error port). If the job run is successful, the component continues processing the next input tokens. Otherwise, the component stops executing other jobs and, from then on, all incoming tokens are ignored and information about ignored tokens is sent to the error output port. This behavior can be changed via the **Stop processing on fail** attribute.

In the case that no input port is attached, only one MapReduce job is executed with default settings specified in the component’s attributes. Both output ports are optional.

For a **MapReduce job execution**, it’s **necessary** to specify at least the following:

- [Hadoop connections](hadoop-connections.md),
- the location of a `.jar` file with classes implementing the MapReduce job,
- the input file and the output directory located on HDFS determined by the selected Hadoop connection,
- the output key/value classes.

These and other (optional) settings could be considered as the default execution settings. However, these default execution settings can be dynamically changed individually for each job execution based on the data from an incoming token. The **Input mapping** attribute is where this override is defined.

After the MapReduce job is finished, the results can be mapped to output ports. Output mapping and error mapping attributes define how output tokens are populated. Information available in job results are comprised mainly of general runtime information and job counters information.

##### Output and error mappings

Both mappings are regular CTL transformations. Output mapping is used to populate the token passed to the first output port. The mapping is executed for successful MapReduce jobs. Error mapping is used only if the job finished unsuccessfully and the second output port is populated instead of the first one.

If output mapping or error mapping is empty, fields of the RunStatus record are mapped to the output by name.

Input data records are the same for both mappings. Two or three records are available:

- The input token which triggered the job execution (not available for component usage without an input connector). This is helpful when you need to pass some fields from the input token to the output token. This record has **Port 0** displayed in the **Type** column.
- JobResults records provide information about the job execution.

| Field Name | Type | Description |
| --- | --- | --- |
| jobID | string | A unique identification given to the job by JobTracker. This value might not be set if the job failed before it was started while contacting the JobTracker. |
| startTime | date | Start date and time of the job. This is measured locally by **CloverDX** and might be slightly different from the job start time measured by JobTracker. Always set. |
| endTime | date | End date and time of the job. This is measured locally by **CloverDX** and might be slightly different from the job end time measured by JobTracker. Always set. |
| duration | long | Duration of the job in milliseconds. This is the difference between **endTime** and **startTime** in milliseconds. May not be greater than the timeout value of the job, if it is set. This value is always set. |
| state | string | The state of the job at the end of its execution.  Possible field values are:  - **SUCCEEDED** if the job was executed successfully, - **FAILED** if the job execution failed, - **TIMEOUT** if the job was killed because its execution time exceeded the specified timeout. |
| clusterErrMessage | string | An error message string as obtained from the JobTracker. |
| errException | string | A textual representation of full stack trace of exception that has occurred on JobTracker or during communication with the JobTracker. This value is not set, if no exception has occurred. |
| lastMapReducePhase | string | The last MapReduce job phase that was in progress when the job ended. The value is one of the following strings: Setup, Map, Reduce or Cleanup. If **wasJobSuccessful** is `true`, then the value is Cleanup. In the case of job failure, this value might be inaccurate if there is a long communication delay to the JobTracker. The actual value can always be obtained using the JobTracker administration site. This value is always set. |
| lastMapReducePhaseProgress | number | The progress of last MapReduce phase that was executing when the job ended. The value is a floating point number inside an interval from 0 to 1, inclusively. If **wasJobSuccessful** is `true`, then the value is 1. In the case of job failure, the value might be inaccurate, especially if there is a considerable communication delay to the JobTracker. Always set. |

- Values of counters handled by the job.

| Field Name | Type | Description |
| --- | --- | --- |
| allCounters | map[string, long] | A map with name/value pairs of all counters available for the job. |
| * | long | All other fields are names of some predefined (default) counters automatically collected by Hadoop for every job. The list of counters might differ depending on the version of Hadoop being used. |

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
| [Job Control comparison](common-of-job-control.md#job-control-comparison) |
