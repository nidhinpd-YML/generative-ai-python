description: Calls the API to initiate a tuning process that optimizes a model for specific data, returning an operation object to track and manage the tuning progress.

<div itemscope itemtype="http://developers.google.com/ReferenceObject">
<meta itemprop="name" content="google.generativeai.create_tuned_model" />
<meta itemprop="path" content="Stable" />
</div>

# google.generativeai.create_tuned_model

<!-- Insert buttons and diff -->

<table class="tfo-notebook-buttons tfo-api nocontent" align="left">
<td>
  <a target="_blank" href="https://github.com/google/generative-ai-python/blob/master/google/generativeai/models.py#L245-L368">
    <img src="https://www.tensorflow.org/images/GitHub-Mark-32px.png" />
    View source on GitHub
  </a>
</td>
</table>



Calls the API to initiate a tuning process that optimizes a model for specific data, returning an operation object to track and manage the tuning progress.


<pre class="devsite-click-to-copy prettyprint lang-py tfo-signature-link">
<code>google.generativeai.create_tuned_model(
    source_model: model_types.AnyModelNameOptions,
    training_data: model_types.TuningDataOptions,
    *,
    id: (str | None) = None,
    display_name: (str | None) = None,
    description: (str | None) = None,
    temperature: (float | None) = None,
    top_p: (float | None) = None,
    top_k: (int | None) = None,
    epoch_count: (int | None) = None,
    batch_size: (int | None) = None,
    learning_rate: (float | None) = None,
    input_key: str = &#x27;text_input&#x27;,
    output_key: str = &#x27;output&#x27;,
    client: (glm.ModelServiceClient | None) = None,
    request_options: (helper_types.RequestOptionsType | None) = None
) -> operations.CreateTunedModelOperation
</code></pre>



<!-- Placeholder for "Used in" -->

Since tuning a model can take significant time, this API doesn't wait for the tuning to complete.
Instead, it returns a `google.api_core.operation.Operation` object that lets you check on the
status of the tuning job, or wait for it to complete, and check the result.

After the job completes you can either find the resulting `TunedModel` object in
`Operation.result()` or `palm.list_tuned_models` or `palm.get_tuned_model(model_id)`.

```
my_id = "my-tuned-model-id"
operation = palm.create_tuned_model(
  id = my_id,
  source_model="models/text-bison-001",
  training_data=[{'text_input': 'example input', 'output': 'example output'},...]
)
tuned_model=operation.result()      # Wait for tuning to finish

palm.generate_text(f"tunedModels/{my_id}", prompt="...")
```

<!-- Tabular view -->
 <table class="responsive fixed orange">
<colgroup><col width="214px"><col></colgroup>
<tr><th colspan="2"><h2 class="add-link">Args</h2></th></tr>

<tr>
<td>
<code>source_model</code><a id="source_model"></a>
</td>
<td>
The name of the model to tune.
</td>
</tr><tr>
<td>
<code>training_data</code><a id="training_data"></a>
</td>
<td>
The dataset to tune the model on. This must be either:
<ul>
<li> A <a href="../../google/generativeai/protos/Dataset.md"><code>protos.Dataset</code></a>, or </li>
<li> An <code>Iterable</code> of:
 <ul>
   <li> <a href="../../google/generativeai/protos/TuningExample.md"><code>protos.TuningExample</code></a>,</li>
   <li> <code>{'text_input': text_input, 'output': output}</code> dicts</li>
   <li> <code>(text_input, output)</code> tuples.</li> 
 </ul>
</li>
<li> A <code>Mapping</code> of <code>Iterable[str]</code> - use <code>input_key</code> and <code>output_key</code> to choose which
  columns to use as the input/output</li>
<li> A csv file (will be read with <code>pd.read_csv</code> and handles as a <code>Mapping</code>
  above). This can be:
 <ul>
  <li> A local path as a <code>str</code> or <code>pathlib.Path</code>.</li>
  <li> A url for a csv file.</li>
  <li> The url of a Google Sheets file.</li>
 </ul>
</li>
<li> A JSON file - Its contents will be handled either as an <code>Iterable</code> or <code>Mapping</code>
  above. This can be:
 <ul>
  <li> A local path as a <code>str</code> or <code>pathlib.Path</code>.</li>
 </ul>
</li>
</td>
</tr><tr>
<td>
<code>id</code><a id="id"></a>
</td>
<td>
The model identifier, used to refer to the model in the API
<code>tunedModels/{id}</code>. Must be unique.
</td>
</tr><tr>
<td>
<code>display_name</code><a id="display_name"></a>
</td>
<td>
A human-readable name for display.
</td>
</tr><tr>
<td>
<code>description</code><a id="description"></a>
</td>
<td>
A description of the tuned model.
</td>
</tr><tr>
<td>
<code>temperature</code><a id="temperature"></a>
</td>
<td>
The default temperature for the tuned model, see <a href="../../google/generativeai/types/Model.md"><code>types.Model</code></a> for details.
</td>
</tr><tr>
<td>
<code>top_p</code><a id="top_p"></a>
</td>
<td>
The default <code>top_p</code> for the model, see <a href="../../google/generativeai/types/Model.md"><code>types.Model</code></a> for details.
</td>
</tr><tr>
<td>
<code>top_k</code><a id="top_k"></a>
</td>
<td>
The default <code>top_k</code> for the model, see <a href="../../google/generativeai/types/Model.md"><code>types.Model</code></a> for details.
</td>
</tr><tr>
<td>
<code>epoch_count</code><a id="epoch_count"></a>
</td>
<td>
The number of tuning epochs to run. An epoch is a pass over the whole dataset.
</td>
</tr><tr>
<td>
<code>batch_size</code><a id="batch_size"></a>
</td>
<td>
The number of examples to use in each training batch.
</td>
</tr><tr>
<td>
<code>learning_rate</code><a id="learning_rate"></a>
</td>
<td>
The step size multiplier for the gradient updates.
</td>
</tr><tr>
<td>
<code>client</code><a id="client"></a>
</td>
<td>
Which client to use.
</td>
</tr><tr>
<td>
<code>request_options</code><a id="request_options"></a>
</td>
<td>
Options for the request.
</td>
</tr>
</table>



<!-- Tabular view -->
 <table class="responsive fixed orange">
<colgroup><col width="214px"><col></colgroup>
<tr><th colspan="2"><h2 class="add-link">Returns</h2></th></tr>
<tr class="alt">
<td colspan="2">
A <a href="https://googleapis.dev/python/google-api-core/latest/operation.html"><code>google.api_core.operation.Operation</code></a>
</td>
</tr>

</table>

