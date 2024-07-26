# Gemini-Fine-Tuning-and-Evaluation
Fine tuning and evalutaion

**Fine Tuning**
Vertex AI Tuning, a service that allows you to improve performance of your LLM in a managed and scalable way. They service is fully based on Vertex AI pipelines to automate the entire tuning process and allowing you to monitoring it thanks to the integration with Vertex AI Tensorboard. 

To tune Gemini 1.0 Pro using either the Vertex AI UI or the Vertex AI SDK for Python. The tuning process requires you to pass the train dataset and optionally a validation dataset. Then you need to define the # of epochs and learning rate multiplier. Finally you launch the job and you monitor its status. 

Notebook:
Gemini_fine_tuning_supervised.ipynb in this repo.

**Evaluation**
For now let’s assume that you tune Gemini 1.0 Pro using  Vertex AI Gemini API to generate your news subhead summaries and you integrate them in your newspapers’ webpage. How can you monitor the capabilities of the model to keep generating them over time?

To address this challenge of Model Evaluation, Vertex AI provides Computation-based and AutoSxS metrics. 

Computation-based and AutoSxS metrics allow you to assess the performance of a model with task-specific metrics computed based on reference data. Also you can use them to compare the performance of 2 models with an arbiter model and verify how they are aligned with human expectations.

Again both metrics are calculated using Vertex AI Pipelines which allows you to schedule evaluation at scale.

To run an AutoSxS evaluation for example you can use Vertex AI Pipeline SDK for Python. 

As you can see, Google Cloud provides an evaluation pipeline template and you just need to provide parameters related to your use case. 

Then you submit a pipeline job which will run the evaluation using Vertex AI Pipeline in a serveless way. 

Model evaluation: 
Pipeline SDK - AutoSxS example code:

from google.cloud import aiplatform
from google_cloud_pipeline_components.preview import model_evaluation
from kfp import compiler

job = aiplatform.PipelineJob(
    job_id=display_name,
    display_name=display_name,
    pipeline_root=str(PIPELINE_ROOT),
    template_path=template_uri,
    parameter_values=parameters,
    enable_caching=False,
)
job.run()


**Notebook using Rapid Evaluation SDK**
Gemini_evaluation_with_rapid_evaluation_sdk.ipynb in this repo.



