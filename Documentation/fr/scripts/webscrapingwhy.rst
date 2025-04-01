
C'est quoi le WebScarping ?
==========================

Le web scraping est une méthode automatique pour obtenir de grandes quantités de données à partir de sites web.
Il existe principalement deux façons **d'extraire des données d'un site web** :

- Utiliser l'API du site web (si elle existe). Par exemple, Facebook dispose de l'API Facebook Graph qui permet de récupérer des données publiées sur Facebook.
- Accéder au HTML de la page web et extraire des informations/données utiles. Cette technique s'appelle le web scraping ou l'extraction de données web.

Pourquoi Python ?
---------------------
Récemment, Python offre un ensemble d'outils et de bibliothèques spécialement conçus pour le web scraping :

1. :doc:`Requests`: Utilisez des bibliothèques comme BeautifulSoup ou lxml pour analyser le HTML et extraire les données pertinentes.

   
2. :doc:`Beautiful-Soup`: XPath est un outil puissant pour naviguer dans les documents XML et HTML. Il vous permet de sélectionner des nœuds ou des éléments dans un document en utilisant des expressions de chemin.

3. :doc:`Selenium` : Les expressions régulières peuvent être utilisées pour extraire des motifs spécifiques des pages web.

Meilleures pratiques
---------------------

Lors du web scraping, il est important de suivre les meilleures pratiques pour éviter d'être bloqué par les sites web :

- Respectez le fichier robots.txt.
- Utilisez une chaîne d'agent utilisateur qui identifie votre scraper.
- Évitez de faire trop de requêtes en peu de temps.
- Soyez attentif aux conditions d'utilisation du site web.

Conclusion
----------

Le web scraping est une technique puissante pour extraire des données des sites web. En utilisant les bonnes techniques et bibliothèques, vous pouvez collecter efficacement les informations dont vous avez besoin pour vos projets.

.. note::
   Cette documentation est uniquement à des fins éducatives. Assurez-vous de respecter les conditions d'utilisation des sites web que vous scrapez.
