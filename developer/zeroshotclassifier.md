<!-- Development > Component reference > AI Components > AIZeroShotClassifier -->

### AIZeroShotClassifier

![AIZeroShotClassifier 64x64](../figures/AIZeroShotClassifier-64x64.png)

| [Short description](zeroshotclassifier.md#short-description) |
| --- |
| [Ports](zeroshotclassifier.md#ports) |
| [Metadata](zeroshotclassifier.md#metadata) |
| [AIZeroShotClassifier attributes](zeroshotclassifier.md#aizeroshotclassifier-attributes) |
| [Compatibility](zeroshotclassifier.md#compatibility) |
| [See also](zeroshotclassifier.md#see-also) |
> [!NOTE]
> This component is currently in the **incubation phase**. Although it is available for use, it is under active development and may be subject to changes. We welcome feedback and encourage users to explore its capabilities.

#### Short description

The **AIZeroShotClassifier** component processes **probabilistic multi-label classification** for user-defined classes; that is, it lets you define your own classes (think of terms, entities, topics, …​) and it will score the input text against them.

For example, you can define classes like "weather", "mood", and "cat" and then for an input text such as "The weather is really nice today", you will get a really high score for "weather", reasonable score for "mood" and negligible score for "cat".

**MODEL WARNING** This component currently only works with Facebook’s BART Zero-Shot Text Classification model - please visit [CloverDX Marketplace](https://marketplace.cloverdx.com) to download a ready-to-use package with the model.

**Performance warning** Zero-shot classification is generally a very expensive operation. Consider using models trained for *pre-defined* classes, which are more efficient. In that case see [AITextClassifier](textclassifier.md).

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1 | **⨯** | **⨯** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 1 | **✓** | The text(s) to classify | At least one `string` field |
| Output | 1 | **⨯** | Copy of the input data + text classification result | Any |

#### Metadata

**AIZeroShotClassifier** propagates input metadata to output.

#### AIZeroShotClassifier attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| **Model** |  |  |  |
| Server model |  | This component currently only works with Facebook’s BART Zero-Shot Text Classification model - please visit [CloverDX Marketplace](https://marketplace.cloverdx.com) to download a ready-to-use package with the model. |  |
| Classification model directory |  | Path to the [machine learning model directory](libraries-dev.md#machine-learning-models). It is required unless **Server model** is defined. |  |
| Model name | no | A read-only field displaying name defined in model configuration files (if available). |  |
| Device | yes | The device to run the model – either processor (CPU) or graphics card (GPU). You must set the device the model is designed for. GPU models are much faster but you need a specialized hardware to use them. | CPU (default) \| GPU |
| Model arguments | no | Configuration arguments for the model. See documentation of your particular model. |  |
| Tokenizer arguments | no | Configuration arguments for the tokenizer. See documentation of your particular model. |  |
| Translator arguments | no | Configuration arguments for the translator. See documentation of your particular model. |  |
| **Input / output parameters** |  |  |  |
| Fields to classify | yes | List of `string` fields to be classified. |  |
| Classes and thresholds | yes | List of user-defined text classes whose score shall be computed. There is no restriction for the class names – they can consist of one word (“medicine“) as well as a phrase or sentence (“medicine, a science or practice of caring for patients, managing the diagnosis, prognosis, prevention and treatment”). Optional thresholds define the minimum score at which the particular class is added to output. |  |
| Classification output field | no | An output field which will store the analysis results. It must be of *variant* type. If the field already contains some analysis, the analyses are merged, so that you can concatenate several AI components and use their combined output. |  |
| Batch size | no | Number of records processed by model together. | an integer number |
| **Error handling** |  |  |  |
| Token overflow policy | no | Specifies behavior when some input text cannot be encoded because it exceeds the model-specific maximum length. The *strict* policy causes the component to fail while *lenient* just logs a warning and truncates the input. | strict (default) \| lenient |
| **Advanced** |  |  |  |
| Transform | no | Set of CTL methods to control what units are used to generate output records. A separate record can be created for each input record, each text–class pair, or both.  For example, you can find the class with the greatest score and only generate output for this class. |  |

#### Compatibility

| Version | Compatibility notice |
| --- | --- |
| 7.1.0 | AIZeroShotClassifier is available since CloverDX version 7.1. |

#### See also

| [AITextClassifier](textclassifier.md) |
| --- |
| [AIZeroShotClassifier](zeroshotclassifier.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
