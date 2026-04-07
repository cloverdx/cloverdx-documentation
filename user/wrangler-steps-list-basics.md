<!-- End user’s guide > Wrangler user guide > Transformation steps > Basics -->

#### Basics

Wrangler provides a wide range of transformation steps that help you clean, validate, enrich, and reshape your data. These steps cover common data preparation tasks such as text and date transformations, calculations, data quality checks, anonymization, filtering, and operations that work with the structure of the data set.

When working with supported transformation steps, you can also use [step preview](wrangler-steps-list-basics.md#step-preview) to inspect the expected result before applying the step. Preview helps you validate the effect of the edited step directly while configuring it, so you can better understand how the step affects your data before saving the change. This is especially useful for steps that use formulas or produce calculated output.

##### Editing steps

When you select a step in Wrangler, its configuration is opened in the sidebar, where you can review and adjust its settings. This allows you to edit the step while keeping the data preview visible, so you can stay in context and immediately see how the configuration relates to your data.

##### Step preview

For supported steps, the editor also provides preview functionality, which helps you inspect the expected output before applying the step.

Inspect the expected result before applying the step to your transformation. This helps you validate changes earlier and better understand how the edited step affects your data.

The preview is shown in a floating panel next to the main data preview. It displays the output produced by the currently edited step together with the related source columns when they are needed for context. This allows you to compare the original values with the previewed result directly during editing.

To load or update the preview, click Generate preview in the step editor. Depending on the edited step, the preview may show one output column or multiple output columns. Preview is available for almost all steps with small exceptions (e.g. Sort, Deduplicate, Group by and few others).

Step preview is designed to make transformation editing easier to understand and easier to validate before the step is applied.

![step preview](../figures/step-preview.gif)
*Figure 104. Step preview showing output of a Lookup step while the step is being edited.*
