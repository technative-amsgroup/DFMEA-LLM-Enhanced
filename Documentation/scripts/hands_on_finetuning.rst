Ok, so now, for educational purposes only, we’re going to start with some hands-on activities just to cement the concepts firmly in our minds. To do that, we're going to be using the following libraries:
- PyTorch (provides the lowest level interface)
- Hugging Face Transformers
- Llama Library

.. note::
   These are not necessarily the libraries we used in the project,
   but they could be a good starting point for anyone looking to explore.

In this first example, we’re going to use the Llama library to import some pre-trained, open-source models hosted on Hugging Face (in this example, it's Llama 2.7). We will compare their outputs before and after fine-tuning them for chatting.

Before chat fine-tuning:
.. code-block:: bash

   pip install llama-library

.. code-block:: python

   from llama import BasicModelRunner

   non_finetuned = BasicModelRunner("meta-llama/Llama-2-7b-hf")
   print(non_finetuned.predict("Tell me how to fix a broken car window"))

After chat fine-tuning:
.. code-block:: python

   finetuned_model = BasicModelRunner("meta-llama/Llama-2-7b-chat-hf")
   print(finetuned_model.predict("Tell me how to fix a broken car window"))

.. note::
   We can fine-tune a model more than once for additional features. As seen here, we fine-tuned the LLM for chatting, but we can also fine-tune it to play, for example, the role of an assistant in a certain company, given their Q&A information or previous assistant-client conversations.

Now, let’s take a look at how the pretraining and fine-tuning data are structured and why.

Pretraining data:
.. code-block:: python

   import jsonlines
   import itertools
   import pandas as pd
   from pprint import pprint

   import datasets
   from datasets import load_dataset
   pretrained_dataset = load_dataset("c4", "en", split="train", streaming=True)

.. _c4: https://huggingface.co/datasets/c4

.. note:: 
   We’re importing the dataset named 'Common Crawl' :c4:. It’s one of the best out there and is open source.
   It contains millions of examples, each one is a JSON object with keys like “id”, “created_at”, “url”, “title”, and it contains all kinds of text. This dataset is available on Hugging Face's dataset hub.

Let's see the first five texts of this dataset, so you can get an idea about what is inside each text:
.. code-block:: python

   n = 5
   print("Pretrained dataset samples:")
   top_n = itertools.islice(pretrained_dataset, n)
   for sample in top_n:
       print(sample)

Company fine-tuning dataset:
.. code-block:: python

   filename = "company_docs.jsonl"
   instruction_dataset_df = pd.read_json(filename, lines=True)
   print(instruction_dataset_df.head())

As we can see, it's more structured in a question-answer format rather than just a pile of unlabeled text. But the data here is in the form of a dataframe with two columns: "Question" and "Answer". To make it compatible for fine-tuning, we have to concatenate the questions and answers like this:
.. code-block:: python

   examples = instruction_dataset_df.to_dict(orient='records')
   text = examples[0]["Question"] + " " + examples[0]["Answer"]
   print(text)

This structured approach, often called a prompt template, is necessary because our model needs to understand context.

.. code-block:: python

   prompt_template_qa = """### Question:\n{question}\n\n### Answer:\n{answer}"""
   # Let's apply it to the whole dataset
   finetuning_dataset = []
   for example in examples:
       text_with_prompt_template_qa = prompt_template_qa.format(question=example["Question"], answer=example["Answer"])
       finetuning_dataset.append({"text": text_with_prompt_template_qa})

And finally, to store the fine-tuning data, we usually opt for the JSONL format:

.. code-block:: python

   with jsonlines.open('company_docs_processed.jsonl', 'w') as writer:
       writer.write_all(finetuning_dataset)

.. note:: 
   We can also upload the dataset directly to Hugging Face for later use.

.. code-block:: python

   finetuning_dataset_name = "your_username/company_docs"
   finetuning_dataset = load_dataset(finetuning_dataset_name)
   print(finetuning_dataset)
