
Practical Fine-Tuning: Practical Guide 🖥
===============================================================

|colab|

.. |colab| image:: ../images/opencolab.png
    :width: 120
    :height: 20
    :target: https://colab.research.google.com/github/MasrourTawfik/DFMEA-LLM-Enhanced/blob/main/COMPARAISON.ipynb
..

.. toctree::
   :maxdepth: 2
   :caption: Steps:

   Preprocessing
   Tokenization
   Training
   Ludwig
   Evaluation

..

Overview
^^^^^^^^^^

Introduction
------------
For educational purposes, we will engage in practical activities to firmly consolidate the concepts in our minds, including code examples and tutorials.

Libraries Used
-----------------------
- **PyTorch**: Provides the lowest-level interface for training deep learning models.
- **Hugging Face Transformers**: Offers pre-trained models and tools for fine-tuning and implementing natural language processing models.
- **Llama Library**

.. note::
   These are not necessarily the libraries we used in the project, but they could be a good starting point for anyone wishing to explore.



In this first example, we will use the Llama library to import some pre-trained and open-source models hosted on Hugging Face (in this example, it is Llama 2.7). We will compare their outputs before and after fine-tuning them for discussion.

Difference between a fine-tuned model and a pre-trained architecture:
------------------------------------

**Pre-trained architecture:**

.. code-block:: bash

   pip install llama-library

.. code-block:: python

   from llama import BasicModelRunner

   non_finetuned = BasicModelRunner("meta-llama/Llama-2-7b-hf")
   print(non_finetuned.predict("Tell me how to fix a broken car window"))


**After chat fine-tuning:**

.. code-block:: python

   finetuned_model = BasicModelRunner("meta-llama/Llama-2-7b-chat-hf")
   print(finetuned_model.predict("Tell me how to fix a broken car window"))

.. note::
We can fine-tune a model more than once for additional features. As seen here, we have fine-tuned the LLM for discussion, but we can also fine-tune it to play, for example, the role of an assistant in a given company, using their Q&A information or previous conversations between assistant and client.





