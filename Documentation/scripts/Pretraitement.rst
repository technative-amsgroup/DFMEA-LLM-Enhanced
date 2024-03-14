Pretraitement des données
===================

Maintenant, regardons comment les données de pré-entraînement et d'affinage sont structurées et pourquoi.

**données de pré-entraînement:**

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


**données d'affinage:**

.. code-block:: python

   filename = "company_docs.jsonl"
   instruction_dataset_df = pd.read_json(filename, lines=True)
   print(instruction_dataset_df.head())

Comme nous pouvons le voir, il est plus structuré sous forme de questions-réponses plutôt que simplement une pile de texte non étiqueté. Mais les données ici sont sous la forme d'un dataframe avec deux colonnes : "Question" et "Réponse". Pour le rendre compatible avec l'affinage, nous devons concaténer les questions et réponses de cette manière :

.. code-block:: python

   examples = instruction_dataset_df.to_dict(orient='records')
   text = examples[0]["Question"] + " " + examples[0]["Answer"]
   print(text)

Cette approche structurée, souvent appelée modèle de prompt, est nécessaire car notre modèle doit comprendre le contexte.

.. code-block:: python

   prompt_template_qa = """### Question:\n{question}\n\n### Answer:\n{answer}"""
   # Let's apply it to the whole dataset
   finetuning_dataset = []
   for example in examples:
       text_with_prompt_template_qa = prompt_template_qa.format(question=example["Question"], answer=example["Answer"])
       finetuning_dataset.append({"text": text_with_prompt_template_qa})

.. attention::
   La plupart du temps, le modèle de prompt Question/Réponse donné n'est pas suffisant ou optimal pour obtenir de bons résultats, donc nous sommes tentés d'utiliser des instructions/input/output ou des modèles supplémentaires.
.. code-block:: python
   prompt_template_with_input = """Below is an instruction that describes a task, paired with an input that provides further context. Write a response that appropriately completes the request.

   ### Instruction:
   {instruction}

   ### Input:
   {input}

   ### Response:"""

   prompt_template_without_input = """Below is an instruction that describes a task. Write a response that appropriately completes the request.

   ### Instruction:
   {instruction}

   ### Response:"""


Et enfin, pour stocker les données d'affinage, nous optons généralement pour le format JSONL :

.. code-block:: python

   with jsonlines.open('company_docs_processed.jsonl', 'w') as writer:
       writer.write_all(finetuning_dataset)

.. note:: 
   Nous pouvons également télécharger le jeu de données directement sur Hugging Face pour une utilisation ultérieure.

.. code-block:: python

   finetuning_dataset_name = "your_username/company_docs"
   finetuning_dataset = load_dataset(finetuning_dataset_name)
   print(finetuning_dataset)
