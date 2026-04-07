<!-- Development > Component reference > Joiners > Common properties of Joiners > Java interfaces for Joiners -->

#### Java interfaces for Joiners

This is used in every **Joiner**, **Map** and **DataIntersection**.

The transformation implements methods of the `RecordTransform` interface and inherits other common methods from the `Transform` interface. See [Common Java interfaces](transformations.md#common-java-interfaces).

Following are the methods of the `RecordTransform` interface:

- `boolean init(Properties parameters, DataRecordMetadata[] sourcesMetadata, DataRecordMetadata[] targetMetadata)`
  Initializes a transformation class/function. This method is called only once at the beginning of transformation process. Any object allocation/initialization should happen here.
- `int transform(DataRecord[] sources, DataRecord[] target)`
  Performs transformation of source records to target records. This method is called as one step in transforming flow of records. For detailed information about return values and their meaning, see [Return values of transformations](transformations.md#return-values-of-transformations).
- `int transformOnError(Exception exception, DataRecord[] sources, DataRecord[] target)`
  Performs transformation of source records to target records. This method is called as one step in transforming flow of records. For detailed information about return values and their meaning, see [Return values of transformations](transformations.md#return-values-of-transformations). Called only if `transform(DataRecord[], DataRecord[])` throws an exception.
- `void signal(Object signalObject)`
  A method which can be used for signalling into transformation that something outside happened. (For example in aggregation component key changed.)
- `Object getSemiResult()`
  A method which can be used for getting intermediate results out of a transformation. May or may not be implemented.
