Lab Learning Objective: In this lab, you will learn how to perform inference with large language models (LLMs) using CPUs and Hugging Face Pipelines. Specifically, you will run Falcon-7b, which has approximately 7.5 billion parameters, on a 4th Generation Xeon CPU. You will also explore using Hugging Face* Pipelines to apply pre-trained models for text generation tasks.


Made using AI with Nightcafe
Value of Exercise: This lab provides hands-on experience optimizing deep learning workflows for CPU-based inference using large language models. Understanding how to choose hardware based on the use case and leveraging high-level interfaces like Hugging Face Pipelines is crucial in AI development.

Access to Intel Developer Cloud Resource: Intel® 4th Generation Xeon – Large VM (Available in Premium Tier - Coupons offered for this tier upon request.)


Image of VM configuration on Intel Developer Cloud
Step-by-step Instructions for the Lab:

Setup
Connect to your Intel Developer Cloud session through the Visual Studio Code application.
If you have not done so, clone the course code repository.
Navigate to the env directory.
The code in the sample directory references this lab.
Use the conda.yml file to build your conda environment to run the sample. Run:

Run the following to activate the environment: 

Understanding the code and workflow (full script image on last page of lab instructions): 
Model Setup:
model = f"tiiuae/falcon-{FLAGS.falcon_version}": Constructs the model identifier based on the Falcon version specified in the command-line arguments.
tokenizer = AutoTokenizer.from_pretrained(model, trust_remote_code=True): Initializes a tokenizer for the specified model, allowing text inputs to be processed for the model.
Pipeline Creation:
generator = transformers.pipeline(...): Creates a text generation pipeline using the transformers library. This pipeline abstracts model loading, tokenization, and inference
Arguments provided to the pipeline creation:
"text-generation": Specifies the pipeline type.
model=model: Specifies the pre-trained model to be used.
tokenizer=tokenizer: Specifies the tokenizer to be used.
torch_dtype=torch.bfloat16: Sets the data type for torch tensors to bfloat16.
trust_remote_code=True: Allows remote code execution for the tokenizer.
device_map="auto": Automatically selects the device for inference.
User Interaction Loop:
user_input = "start": Initializes the user input to begin the loop.
while user_input != "stop":: Starts a loop that continues until the user enters "stop".
User Input and Inference:
user_input = input(...): Prompts the user to input a text string for the model to generate text based on.
Generating Sequences:
sequences = generator(...): Generates text sequences using the pre-trained model and provided input.
f""" {user_input}""": Formats the user input for model processing.
max_length=FLAGS.max_length: Specifies the maximum length of the generated text.
do_sample=False: Disables sampling during text generation.
top_k=FLAGS.top_k: Sets the number of highest probability tokens to consider.-
num_return_sequences=1: Specifies the number of generated sequences to return.
eos_token_id=tokenizer.eos_token_id: Specifies the end-of-sequence token ID.
Running Falcon with Hugging Face Pipelines:
We will use a Python script named falcon-demo.py to run Falcon inference with Hugging Face Pipelines.
 Open the Falcon_HF_Pipelines.py script using a text editor or integrated development environment (IDE) to understand its contents and functionality.
 The script uses the transformers library to load a pre-trained Falcon model and create a text generation pipeline.
 You can configure parameters like Falcon version, max length, and top k for text generation.
 Run the script in the terminal with your desired parameters: 

Experiment with Raw Falcon:
While interacting with the script, note that Raw Falcon may produce nonsensical output.
The script reports the inference time, which shows how long the model takes to respond based on parameters and available compute.
You can modify the max_length parameter to observe its impact on inference time.
To end the interaction, type "stop".
Challenge Questions:

How does using Hugging Face Pipelines simplify the process of applying pre-trained models to NLP tasks?
What is the purpose of being a "Compute Aware AI Developer"? Explain in your own words.
 

Challenge Question Answers:

Hugging Face Pipelines abstract away the complexities of working with pre-trained models for NLP tasks. They provide a high-level interface that simplifies tasks like model loading, tokenization, and inference. Developers can quickly apply state-of-the-art models to their tasks with minimal code, without needing an in-depth understanding of the model's intricacies. This speeds up development and experimentation processes.
Being a "Compute Aware AI Developer" means considering the requirements and goals of your AI application before choosing the appropriate hardware and software stack. Instead of blindly opting for the most powerful hardware, this approach involves selecting hardware based on the application's specific needs, which can lead to better performance and cost-efficiency.