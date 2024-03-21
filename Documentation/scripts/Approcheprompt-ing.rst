Approche prompt engineering 💭
------------------------

Dans le cadre de notre projet, nous devrons trouver une technique de prompte
engineering éfficace pour pouvoir générer notre table en se basant sur l’input de
l’utilisateur.
Pour cela, nous avons opté pour le one-shot, car notre modèle étant déjà très
performant, n’avait pas besoin de beaucoup d’exemple pour comprendre la tâche à
réaliser. Voici la structure de notre prompt
Système : Il s’agit des instructions fournies au modèle concernant son comportement et la manière dont il devrait se percevoir.
Exemple : C’est une illustration de prompt complétion servant de référence
pour le modèle lors de la génération de ses réponses. Il est composé de deux parties :
— UserContent : Exemple de l’entrée utilisateur.
— ModelResponse : Un exemple de réponse idéale que le modèle est censé
produire.
Complétion : C’est la réponse du modèle à la requête de l’utilisateur, prenant
en considération non seulement son prompt initial, mais également l’exemple de
prompt fourni dans le contexte, ainsi que les instructions spécifiées au niveau du
système. Le processus est resumé dans cette figure:

.. image:: ../images/completion_diagram.png
    :width: 100%
    :align: center
    :alt: completion_diagram
..
