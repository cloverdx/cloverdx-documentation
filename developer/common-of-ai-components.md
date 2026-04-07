<!-- Development > Component reference > AI Components > Common properties of AI components -->

### Common properties of AI components
> [!TIP]
> For customers looking to explore the capabilities of AI components, the setup can be accelerated by using the [official Docker image for AI workloads](https://hub.docker.com/r/cloverdx/cloverdx-server-ai). This image includes a pre-configured CloverDX Server as well as drivers and additional software needed to take advantage of hardware acceleration of AI workloads. The image must be deployed on a machine with NVIDIA GPU to use the GPU acceleration.

#### Model

AI components which use locally hosted models require you to specify the model you want to use. The choice of model determines the capabilities of the components.

Models are not distributed as part of the core product and need to be downloaded and deployed to CloverDX Server by the admin before use. You can provide your own model (some configuration required - for experienced users) or choose from a curated set of free, ready-to-use models available in our online [CloverDX Marketplace](https://marketplace.cloverdx.com) (recommended).

Models from the CloverDX Marketplace are provided as libraries you can install to your CloverDX Server. Once installed, the model will be available to the components via Server model property, no further configuration is required.

- **Server model**: (Recommended) In a Server project, select pre-configured models available from libraries installed on the Server. Go to [CloverDX Marketplace](https://marketplace.cloverdx.com) to download models you need and install them on the Server.
- **Classification model directory**: (for experienced users) The model can be also specified as URI of its directory. For details, see [Machine Learning Models](libraries-dev.md#machine-learning-models).

Models downloaded from the CloverDX Marketplace and selected via **Server model** property will automatically configure the following model properties.

**Model name** is a read-only property which shows the name from model configuration files.

**Device** determines whether the model is run on processor (*CPU*) or graphics card (*GPU*). Processing on GPU is much faster but you need a specialized hardware to use it.

**Model arguments**, **Tokenizer arguments** and **Translator arguments** allow to modify model behavior. They are mode-dependent.

#### Input/output parameters

**Fields to classify** specify fields to be analyzed.

Token/text **classes and thresholds** allow to define classes whose scores shall be computed. The threshold specifies the minimum score at which the class will be included in the output.

**Classification output field** sets an output field which will store the analysis results. It must be of *variant* type. If the field already contains some analysis, the analyses are merged, so that you can concatenate several AI components and use their combined output.

**Batch size** sets number of records processed by model together.

#### Error handling

**Token overflow policy** determines what happens when some input field value cannot be encoded because it exceeds the model-specific maximum length. The *strict* policy causes the component to fail while *lenient* just logs a warning and truncates the input.

#### Advanced

**Transform** allows to control what units are used to generate output records. A separate record can be created for each input record, each sequence-class pair, or both.

#### Cache

To change the [default DJL cache directories](https://djl.ai/docs/development/cache_management.html), use [`DJL_CACHE_DIR`](../admin/list-of-properties.md#lop-ai-djl-cache-dir) and [`ENGINE_CACHE_DIR`](../admin/list-of-properties.md#lop-ai-engine-cache-dir) as system properties or environment variables.

#### AI component execution and model caching

This feature is designed to prevent native memory leaks that may occur when AI models are repeatedly loaded and unloaded. By caching models for the lifetime of the Java process and controlling prediction execution via a dedicated thread pool, the system ensures stable and predictable memory usage during inference.

##### Model caching

By default, once a model is loaded and used by an AI component, it is cached in memory and remains there for the lifetime of the Java process (i.e., it is never unloaded). Model caching is controlled by the [`cloverdx.ai.caching`](../admin/list-of-properties.md#lop-ai-caching) configuration property.

##### Prediction thread pool

Inference tasks are executed in a fixed-size thread pool. This pool isolates prediction work to dedicated threads.

The default pool size is `4`, which limits the number of AI components that can run concurrently. If more AI components attempt to run in parallel, the components that do not fit into the pool will wait for their slot in the pool (i.e., for one of the components that occupy the pool to finish processing).

The pool itself is controlled by the [`cloverdx.ai.pool`](../admin/list-of-properties.md#lop-ai-pool) property. You can modify the pool size by using the [`cloverdx.ai.pool.size`](../admin/list-of-properties.md#lop-ai-pool-size) configuration property.
