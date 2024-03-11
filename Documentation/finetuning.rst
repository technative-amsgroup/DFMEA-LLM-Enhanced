Fine tuning 
====================================

C'est quoi d'abord le finetuning?
-------------------------
Le fine-tuning est un processus itératif visant à améliorer la performance d'un modèle sur une tâche spécifique tout en préservant
 les connaissances préalablement acquises lors de l'entraînement initial. Cette approche repose sur la capacité du modèle à généraliser 
 à de nouveaux domaines tout en conservant sa capacité à se spécialiser. En ajustant les poids des connexions entre les neurones,
le fine-tuning permet d'adapter le modèle à la nouvelle tâche sans altérer de manière significative les connaissances pré-existantes.

.. image:: images/finetuning_01.png
   :alt: fine-tuning

Prenons par exemple un modèle de langage naturel standard. Bien qu'il puisse répondre à vos questions spécifiques concernant un certain domaine, la réponse reste généralement vague. En revanche, si nous le finetunons sur des données spécifiques à ce domaine, la réponse sera transformée de manière à être plus précise et détaillée.

.. image:: images/finetuning_02.png
   :alt: fine-tuning

Les avantages du fine-tuning
------------------------------

- Guide le modèle vers des sorties plus consistantes.
- Réduit les hallucinations.
- Personnalise le modèle à un cas d'utilisation spécifique.
- Le processus est similaire à la formation antérieure du modèle.
- gogo