Entrainement du modèle 
=====================

|colab|

.. |colab| image:: ../images/opencolab.png
    :width: 120
    :height: 20
    :target: https://colab.research.google.com/github/MasrourTawfik/DFMEA-LLM-Enhanced/blob/main/Documentation/colabs/COMPARAISON.ipynb
..


Maintenant, pour entraîner un modèle sur ce jeu de données, nous pouvons simplement utiliser la bibliothèque de haut niveau Llama.


.. code-block:: python
   from llama import BasicModelRunner
   model = BasicModelRunner("EleutherAI/pythia-410m") 
   model.load_data_from_jsonlines("lamini_docs.jsonl", input_key="question", output_key="answer")
   model.train(is_public=True) 

Bien sûr ! Si vous souhaitez une compréhension plus approfondie de ce qui se passe sous le capot, nous pouvons passer à une méthode plus bas niveau.

.. code-block:: python
   import datasets
   import tempfile
   import logging
   import random
   import config
   import os
   import yaml
   import time
   import torch
   import transformers
   import pandas as pd
   import jsonlines

   from utilities import *
   from transformers import AutoTokenizer
   from transformers import AutoModelForCausalLM
   from transformers import TrainingArguments
   from transformers import AutoModelForCausalLM
   from llama import BasicModelRunner


   logger = logging.getLogger(__name__)
   global_config = None

   dataset_name = "lamini_docs.jsonl"
   dataset_path = f"/content/{dataset_name}"
   use_hf = False

   model_name = "EleutherAI/pythia-70m"

   device_count = torch.cuda.device_count()
   if device_count > 0:
      logger.debug("Select GPU device")
      device = torch.device("cuda")
   else:
      logger.debug("Select CPU device")
      device = torch.device("cpu")

   max_steps = 3
   trained_model_name = f"lamini_docs_{max_steps}_steps"
   output_dir = 
   
   training_args = TrainingArguments(

   # Learning rate
   learning_rate=1.0e-5,

   # Number of training epochs
   num_train_epochs=1,

   # Max steps to train for (each step is a batch of data)
   # Overrides num_train_epochs, if not -1
   max_steps=max_steps,

   # Batch size for training
   per_device_train_batch_size=1,

   # Directory to save model checkpoints
   output_dir=output_dir,

   # Other arguments
   overwrite_output_dir=False, # Overwrite the content of the output directory
   disable_tqdm=False, # Disable progress bars
   eval_steps=120, # Number of update steps between two evaluations
   save_steps=120, # After # steps model is saved
   warmup_steps=1, # Number of warmup  steps for learning rate scheduler
   per_device_eval_batch_size=1, # Batch size for evaluation
   evaluation_strategy="steps",
   logging_strategy="steps",
   logging_steps=1,
   optim="adafactor",
   gradient_accumulation_steps = 4,
   gradient_checkpointing=False,

   # Parameters for early stopping
   load_best_model_at_end=True,
   save_total_limit=1,
   metric_for_best_model="eval_loss",
   greater_is_better=False
   )

   model_flops = (
   base_model.floating_point_ops(
      {
         "input_ids": torch.zeros(
            (1, training_config["model"]["max_length"])
         )
      }
   )
   * training_args.gradient_accumulation_steps
   )

   print(base_model)
   print("Memory footprint", base_model.get_memory_footprint() / 1e9, "GB")
   print("Flops", model_flops / 1e9, "GFLOPs")

   trainer = Trainer(
    model=base_model,
    model_flops=model_flops,
    total_steps=max_steps,
    args=training_args,
    train_dataset=train_dataset,
    eval_dataset=test_dataset,
   )

   training_output = trainer.train()

   save_dir = f'{output_dir}/final'

   trainer.save_model(save_dir)
   print("Saved model to:", save_dir)

.. note:: 
   Maintenant, nous pouvons recharger le modèle pour nos besoins de la manière suivante :
   
.. code-block:: python
   finetuned_model = AutoModelForCausalLM.from_pretrained(save_dir, local_files_only=True)
