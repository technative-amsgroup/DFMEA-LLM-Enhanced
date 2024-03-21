
Requests Guide
==============

Introduction
------------

The `requests` module is a popular Python library used for making HTTP requests. It provides a simple and intuitive API for sending HTTP requests and handling responses. This guide will explain the basic principles of using the `requests` module for web scraping.

Installation
------------

To use the `requests` module, you need to install it first. You can install it using `pip`, the Python package installer, by running the following command:

.. code-block:: bash

    pip install requests

Making GET Requests
-------------------

The most common type of HTTP request is the GET request, which is used to retrieve data from a server. The `requests` module makes it easy to send GET requests. Here's an example:

.. code-block:: python

    import requests

    response = requests.get('https://www.example.com')

    print(response.status_code)  # Print the status code
    print(response.text)         # Print the response content

Making POST Requests
--------------------

In addition to GET requests, you can also send POST requests using the `requests` module. POST requests are used to send data to a server. Here's an example:

.. code-block:: python

    import requests

    data = {'username': 'john', 'password': 'secret'}
    response = requests.post('https://www.example.com/login', data=data)

    print(response.status_code)  # Print the status code
    print(response.text)         # Print the response content

Handling Response
-----------------

After sending a request, you can access the response object returned by the `requests` module. The response object provides various attributes and methods to access the response data. Here are a few examples:

- `response.status_code`: The HTTP status code of the response.
- `response.text`: The response content as a string.
- `response.json()`: If the response content is JSON, this method returns the parsed JSON data.

Error Handling
--------------

When working with requests, it's important to handle errors properly. The `requests` module raises exceptions for common errors, such as network errors or invalid URLs. You can use try-except blocks to handle these exceptions. Here's an example:

.. code-block:: python

    import requests

    try:
         response = requests.get('https://www.example.com')
         response.raise_for_status()  # Raise an exception if the request was unsuccessful
    except requests.exceptions.RequestException as e:
         print('An error occurred:', e)

Conclusion
----------

The `requests` module is a powerful tool for making HTTP requests in Python. It provides a simple and intuitive API for sending requests and handling responses. With the knowledge gained from this guide, you should be able to start using the `requests` module for web scraping and other HTTP-related tasks.
