<!-- Development > Component reference > AI Components > AITextClassifier -->

### AITextClassifier

![AITextClassifier 64x64](../figures/AITextClassifier-64x64.png)

| [Short description](textclassifier.md#short-description) |
| --- |
| [Ports](textclassifier.md#ports) |
| [Metadata](textclassifier.md#metadata) |
| [AITextClassifier attributes](textclassifier.md#aitextclassifier-attributes) |
| [Compatibility](textclassifier.md#compatibility) |
| [See also](textclassifier.md#see-also) |
> [!NOTE]
> This component is currently in the **incubation phase**. Although it is available for use, it is under active development and may be subject to changes. We welcome feedback and encourage users to explore its capabilities.

#### Short description

The **AITextClassifier** component processes **probabilistic multi-label classification**; that is, it scores input text field(s) against pre-trained set of classes.

The list of classes the component is able to identify and score is determined by the model.

For example, with a model trained for sentiment analysis, the component will be able to return two classes (POSITIVE, NEGATIVE) and corresponding probabilistic scores for each.

If you want to define your own classes, see [AIZeroShotClassifier](zeroshotclassifier.md).

For more granular classification within text (tokens), see [AITokenClassifier](tokenclassifier.md).

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1 | **⨯** | **⨯** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 1 | **✓** | The text(s) to classify | At least one `string` field |
| Output | 1 | **⨯** | Copy of the input data + text classification result | Any |

#### Metadata

**AITextClassifier** propagates input metadata to output.

#### AITextClassifier attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| **Model** |  |  |  |
| Server model |  | Recommended: Use a model installed as a library on the CloverDX Server. Check [CloverDX Marketplace](https://marketplace.cloverdx.com) for available ready-to-use models. This is a more convenient alternative to **Classification model directory**. |  |
| Classification model directory |  | Path to the [machine learning model directory](libraries-dev.md#machine-learning-models). It is required unless **Server model** is defined. |  |
| Model name | no | A read-only field displaying name defined in model configuration files (if available). |  |
| Device | yes | The device to run the model – either processor (CPU) or graphics card (GPU). You must set the device the model is designed for. GPU models are much faster but you need a specialized hardware to use them. | CPU (default) \| GPU |
| Model arguments | no | Configuration arguments for the model. See documentation of your particular model. |  |
| Tokenizer arguments | no | Configuration arguments for the tokenizer. See documentation of your particular model. |  |
| Translator arguments | no | Configuration arguments for the translator. See documentation of your particular model. |  |
| **Input / output parameters** |  |  |  |
| Fields to classify | yes | List of `string` fields to be classified. |  |
| Text classes and thresholds | no | List of text classes whose score shall be computed. The classes are model-dependent; you can use only some of them, but you cannot add classes unknown to the model ([AIZeroShotClassifier](zeroshotclassifier.md) servers for this purpose). Optional thresholds define the minimum score at which the particular class is added to output.  If not specified, AITextClassifier uses all classes defined by the model. |  |
| Classification output field | no | An output field which will store the analysis results. It must be of *variant* type. If the field already contains some analysis, the analyses are merged, so that you can concatenate several AI components and use their combined output. |  |
| Batch size | no | Number of records processed by model together. | an integer number |
| **Error handling** |  |  |  |
| Token overflow policy | no | Specifies behavior when some input text cannot be encoded because it exceeds the model-specific maximum length. The *strict* policy causes the component to fail while *lenient* just logs a warning and truncates the input. | strict (default) \| lenient |
| **Advanced** |  |  |  |
| Transform | no | Set of CTL methods to control what units are used to generate output records. A separate record can be created for each input record, each text–class pair, or both.  For example, you can find the class with the greatest score and only generate output for this class. |  |

#### Compatibility

| Version | Compatibility notice |
| --- | --- |
| 7.1.0 | AITextClassifier is available since CloverDX version 7.1. |

#### See also

| [AITokenClassifier](tokenclassifier.md) |
| --- |
| [AIZeroShotClassifier](zeroshotclassifier.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
