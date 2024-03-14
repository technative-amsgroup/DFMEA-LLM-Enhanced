
Affinage Pratique : Guide Pratique
===============================================================

Introduction
------------
Pour des fins éducatives, nous allons nous lancer dans des activités pratiques afin de consolider fermement les concepts dans nos esprits, en incluant des exemples de code et des tutoriels.

Bibliothèques Utilisées
-----------------------
- **PyTorch** : Fournit l'interface de plus bas niveau pour l'entraînement de modèles de deep learning.
- **Transformers de Hugging Face** : Propose des modèles pré-entraînés et des outils pour le fine-tuning et l'implémentation de modèles de traitement du langage naturel.
- **Llama Library**

.. note::
   Ce ne sont pas nécessairement les bibliothèques que nous avons utilisées dans le projet, mais elles pourraient être un bon point de départ pour quiconque souhaite explorer.



Dans cet premier exemple, nous allons utiliser la bibliothèque Llama pour importer quelques modèles pré-entraînés et open source hébergés sur Hugging Face (dans cet exemple, il s'agit de Llama 2.7). Nous comparerons leurs sorties avant et après les avoir affinés pour la discussion.

Difference entre un modèle finetuné et une architecture pré-entrainée:
------------------------------------

**architecture pré-entrainé:**

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
Nous pouvons affiner un modèle plus d'une fois pour des fonctionnalités supplémentaires. Comme on le voit ici, nous avons affiné le LLM pour la discussion, mais nous pouvons également l'affiner pour jouer, par exemple, le rôle d'un assistant dans une entreprise donnée, en utilisant leurs informations de questions-réponses ou des conversations précédentes entre assistant et client.

.. toctree::
    :maxdepth: 2
    :caption: Contents:

    Pretraitement
    tokenisation
    Entrainement
    


