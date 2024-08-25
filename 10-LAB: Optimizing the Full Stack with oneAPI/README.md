Lab Duration: 30 min

Lab Learning Objective: Learn how to enhance inference with oneAPI optimizations.

Problem Statement: The team has successfully run the predictive maintenance solution in production for a few months. Fancy Orchards has purchased additional land to increase production and support growing demand. An increase in production means additional equipment. Tracking additional machines in the predictive maintenance tool has impacted latency due to the increased load of real-time inference requests.

Your leadership is considering purchasing additional infrastructure to handle the load. In a stroke of genius, you recall the principles of software-hardware co-design and decide to research what kind of optimizations could help improve inference performance without the additional infrastructure investment.


Made using AI with Nightcafe
You come across oneAPI optimizations for XGBoost models through the oneDAL library. On a similar workload, the oneDAL optimizations demonstrate up to ~50% prediction speedup over stock. You aim to implement the optimizations required to convert our XGBoost model to daal4py format to optimize the inference workload. Upon completing this step, you will have taken your application from a rudimentary set of APIs to a hardware-optimized prototype with essential MLOps components.

Value of Exercise:

The lab provides hands-on experience in enhancing AI inference performance by leveraging oneAPI optimizations for XGBoost models, ultimately transforming basic APIs into a hardware-optimized prototype with MLOps components.

Access to Intel Developer Cloud Resource: Intel® 4th Generation Xeon VM


Image of VM configuration on Intel Developer Cloud
 

Step-by-step Instructions for the Lab:

Setup
Connect to your Intel Developer Cloud session through the Visual Studio Code application.
If you have not done so, clone the course code repository.
Navigate to the env directory.
Use the code in the sample directory to reference this lab.
Use the "conda.yml file to build your conda environment to run the sample. Run: 

Run the following code to activate the environment:

Visit previous labs for a refresher on MLflow.
We pick up where we left off in the "Building an Inference Endpoint using FastAPI" Lab. Let's review the changes and additions to the sample code:
In the train.py module:

We use the d4p.get_gbt_model_from_xgboost(xgb_model) function to convert the XGBoost model to daal4py format.
We use the mlflow.log_artifact(self.model_path) function to log the daal4py model as an artifact for retrieval during inference.
We added an inference.py module: This function downloads the model artifacts, processes raw data for inference, and yields maintenance predictions.

We use the mlflow.artifacts.download_artifacts() to retrieve the scaler file and daal4py model object.

Create an experiment and training run by running: 


Run the following in the command line to perform inference with the oneDAL optimized model:


Let's unpack this payload:
model_run_id: run id associated with the desired model.
scaler_file_name name of the scaler file that was logged to mlflow.
scaler_destination: path to save the downloaded scaler.
d4p_file_name: name of the d4p model file that was logged to mlflow.
d4p_destination: path to save the downloaded d4p model.
data: the raw sensor data values

Upon running this payload, we should see the following happen:
The scaler and d4p model are retrieved and stored in the current directory.
Preprocess the raw data from the payload.
Generate predictions.
Postprocessing of predictions to generate an interpretable message.
Shutdown Instructions:

Start by suspending the FastAPI uvicorn server but going to the associated terminal and holding CTRL-C on your keyboard.
Next, suspend the MLFlow UI by holding CTRL-C in the associated terminal.
Challenge Questions:

What is the primary objective of using oneAPI optimizations with the oneDAL library in this lab?
Briefly explain the role of the "d4p.get_gbt_model_from_xgboost(xgb_model)" function in the lab's context.
Challenge Question Answers:

The primary objective is to enhance the performance of AI inference by converting and optimizing XGBoost models, utilizing oneAPI optimizations provided by the oneDAL library.
The "d4p.get_gbt_model_from_xgboost(xgb_model)" function is used to convert the XGBoost model to daal4py format, allowing for optimization and improved inference performance using oneAPI optimizations through the oneDAL library.
 