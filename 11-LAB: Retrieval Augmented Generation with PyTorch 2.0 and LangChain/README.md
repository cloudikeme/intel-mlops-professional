Lab Duration: 45 min

Lab Learning Objective: To learn how to implement an LLM pipeline using PyTorch 2.0 and LangChain for in-context learning.

Problem Statement: Fancy Orchards is experiencing unprecedented success, with its apple products rapidly filling grocery store shelves. However, the increased production volume is straining the orchard's automated apple-picking machinery, leading to frequent maintenance requirements. It takes 6 to 10 hours for a specialized expert to travel to the orchards and perform the necessary repairs. While an in-house maintenance crew exists, they lack the specialized knowledge required to handle the machinery.

To address this issue, your team aims to develop a chatbot to assist the in-house crew. This chatbot will act as an "expert-on-demand," providing guided instructions for basic maintenance tasks for the apple-picking machinery.


Made using AI with Nightcafe
Given budget constraints, fine-tuning a large language model for this use case is not feasible. Your team has decided to augment a pre-existing language model with in-context learning and retrieval-augmented generation (RAG) capabilities to overcome this limitation.

Your task is to implement this augmented chatbot using PyTorch 2.0 and LangChain. The chatbot should be capable of providing contextually accurate and specific guidance by leveraging a dataset of historical conversations between specialized maintenance experts and field crews concerning the upkeep of apple-picking machinery.

Value of Exercise: The lab will demonstrate the value of retrieval-augmented text generation in improving the quality and relevance of the generated text. Participants will learn how to implement a retrieval mechanism using LangChain to retrieve similar text snippets and use them to enhance text generation with PyTorch 2.0. Retrieval-augmented generation can lead to more coherent and contextually relevant responses in language models.

Access to Intel Developer Cloud Resource:  Intel® 4th Generation Xeon – Large VM or Bare Metal Instance (Available in Premium Tier - Coupons offered for this tier upon request.)


Baremetal Instance Config on the Intel Developer Cloud
Step-by-step Instructions for the Lab:

Setup
Connect to your Intel® Developer Cloud session through the Visual Studio Code application.
If you have not done so, clone the course code repository.
Navigate to the sample directory.
Create a docker image by running: 

Start the container by running: 

With the container running, copy and paste the following into your browser http://localhost:5000/docs
This opens the FastAPI swagger. Swagger is a built-in web UI for interacting with FastAPI endpoints. We can use it to interact with our model instead of CURL.

Sample FastAPI swagger. This is just a sample image; your endpoint names will be different.
When you send the request, you can track the logs in the terminal to track the similarity search process and general model processing.
You are encouraged to test different queries, adjust the parameters in the script, and evaluate the impact on performance.
If you prefer to use CURL, here is a sample command:



Let's review the PickerBot.py Python module and PickerBot class.
The data_proc() method handles the downloading and processing of our reference dataset. This dataset will contain the information we retrieve for our in-context learning pipeline.
The create_vectorstore() method creates the vector database using Chromadb and Langchain.
The inference() method takes in the user's query, provides it to the similarity search algorithm, and retrieves the relevant information for the vector DB. It then uses the PromptTemplate() function to embed context and the user's query before passing it to the model.
Things to try in this lab:
In the PickerBot class, try changing the prompt template and see if that improves the quality of the responses.
Try to optimize the performance of the chatbot by:
Adjust parameters like chunk_size and overlap in the create_vectorstore() method
In sever.py module, adjust the max_tokens, repeat_penalty, and n_threads in the load_gpt4allj() function.
Remember to rebuild your docker image every time you change the underlying application.
Challenge Questions:

How can retrieval-augmented text generation improve the coherence and relevance of language model responses?
Explain the role of LangChain in the retrieval mechanism for retrieval-augmented text generation.
What are the potential challenges or limitations of using retrieval-augmented text generation in language models?
How can you evaluate the performance of a retrieval-augmented text generation system?
 

Challenge Question Answers:

Retrieval-augmented text generation enhances responses by incorporating relevant context from similar text snippets retrieved from a database. This helps the language model generate more coherent and contextually appropriate responses, improving the overall quality of the generated text.
LangChain plays a key role in the retrieval mechanism by querying a database of text snippets based on the input query. It ranks the retrieved snippets according to similarity and relevance and then provides the top-ranked snippets to the language model for fine-tuning and context enhancement during text generation.
Some challenges of retrieval-augmented text generation include finding an appropriate balance between retrieved context and the model's original generation, dealing with out-of-context responses, and ensuring that retrieved snippets are truly relevant and accurate representations of the input query.
The performance of a retrieval-augmented text generation system can be evaluated using metrics like BLEU score, ROUGE score, and human evaluations to assess the quality, relevance, and coherence of the generated responses.
 