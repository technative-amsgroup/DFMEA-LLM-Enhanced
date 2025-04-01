Guide des requêtes
==================

Introduction
------------

Le module `requests` est une bibliothèque Python populaire utilisée pour effectuer des requêtes HTTP. Il fournit une API simple et intuitive pour envoyer des requêtes HTTP et gérer les réponses. Ce guide expliquera les principes de base de l'utilisation du module `requests` pour le web scraping.

Installation
------------

Pour utiliser le module `requests`, vous devez d'abord l'installer. Vous pouvez l'installer à l'aide de `pip`, l'installateur de packages Python, en exécutant la commande suivante :

.. code-block:: bash

    pip install requests

Effectuer des requêtes GET
--------------------------

Le type de requête HTTP le plus courant est la requête GET, qui est utilisée pour récupérer des données à partir d'un serveur. Le module `requests` facilite l'envoi de requêtes GET. Voici un exemple :

.. code-block:: python

    import requests

    response = requests.get('https://www.example.com')

    print(response.status_code)  # Affiche le code d'état
    print(response.text)         # Affiche le contenu de la réponse

Effectuer des requêtes POST
---------------------------

En plus des requêtes GET, vous pouvez également envoyer des requêtes POST à l'aide du module `requests`. Les requêtes POST sont utilisées pour envoyer des données à un serveur. Voici un exemple :

.. code-block:: python

    import requests

    data = {'username': 'john', 'password': 'secret'}
    response = requests.post('https://www.example.com/login', data=data)

    print(response.status_code)  # Affiche le code d'état
    print(response.text)         # Affiche le contenu de la réponse

Gestion des réponses
--------------------

Après avoir envoyé une requête, vous pouvez accéder à l'objet de réponse renvoyé par le module `requests`. L'objet de réponse fournit divers attributs et méthodes pour accéder aux données de réponse. Voici quelques exemples :

- `response.status_code` : Le code d'état HTTP de la réponse.
- `response.text` : Le contenu de la réponse sous forme de chaîne de caractères.
- `response.json()` : Si le contenu de la réponse est au format JSON, cette méthode renvoie les données JSON analysées.

Gestion des erreurs
-------------------

Lorsque vous travaillez avec des requêtes, il est important de gérer les erreurs correctement. Le module `requests` génère des exceptions pour les erreurs courantes, telles que les erreurs réseau ou les URL invalides. Vous pouvez utiliser des blocs try-except pour gérer ces exceptions. Voici un exemple :

.. code-block:: python

    import requests

    try:
         response = requests.get('https://www.example.com')
         response.raise_for_status()  # Génère une exception si la requête a échoué
    except requests.exceptions.RequestException as e:
         print("Une erreur s'est produite :", e)
         
Conclusion
----------

Le module `requests` est un outil puissant pour effectuer des requêtes HTTP en Python. Il fournit une API simple et intuitive pour envoyer des requêtes et gérer les réponses. Avec les connaissances acquises grâce à ce guide, vous devriez être en mesure de commencer à utiliser le module `requests` pour le web scraping et d'autres tâches liées à HTTP.
