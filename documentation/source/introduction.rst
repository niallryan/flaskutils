Flask-Philo
=============

Utilities to build flask based microservices.

What this project is about?
---------------------------

Flask is an awesome web microframework that works great out of the box. Nevertheless,
additional configuration and integration with complimentary libraries is required in
order to build complex applications. Here at `Riffstation <https://play.riffstation.com/>`_
we have several HTTP REST-based microservices and whenever we want to create a new
microservice we need to bootstrap very similar common code.

This library wants to concentrate all logic related with HTTP, REST, databases in one common place.
Feel free to use it and extend it. We are willing to hear about your suggestions and improvements.


Basic Features
--------------

- REST out of the box.

- Simple sqlalchemy orm customized for postgresql with multiple dabatases.

- Simple Redis integration.

- Simple Elastic Search integration.

- Basic AWS integration.


Quick start
------------

Installation
############

::

    pip install Flask-Philo


Alternatively, you can create a virtual environment first:

::

    mkvirtualenv -p /usr/bin/python3 philo
    pip install Flask-Philo


Creating a new project
######################

Flask-Philo includes the ``flask-philo-admin`` command line tool.

To quickly generate a new Flask-Philo project, navigate to the directory in which you want to create the project and run:

::

    flask-philo-admin startproject <project_name>


This will create a folder called <project_name> which will contain the basic structure of a Flask-Philo application.

Example:

::

    flask-philo-admin startproject flask-philo-example


Folder structure
################

Here follows the folder structure for the recent created project:

* README.md
* documentation
* src
    * app
        * __init__.py
        * models
        * serializers
        * urls.py
        * views
    * config
        * development.py
        * test.py
    * console_commands
        * __init__.py
    * manage.py
    * tests
        * __init__.py
        * test_views.py
* tools
    * requirements
        * base.txt
        * dev.txt

Running the server for the new project_name
###########################################

In order to run the server for the new project, you should go the ``src`` folder:

::

    flask-philo-example > cd src

And run the following command:

::

    python3 manage.py runserver

The response from this command will be something like this:

::

    * Running on http://0.0.0.0:8080/ (Press CTRL+C to quit)
    * Restarting with stat
    * Debugger is active!
    * Debugger PIN: 147-416-135

To access the server, you will have to take a look in two concepts: URLs and view files.

URLs
####

The urls file contains all the routes of the service. You can refer to the example created automatically by Flask-Philo by accessing the file ``urls.py`` located in the ``src/app``. It will look like this:

::

    from app.views.example_views import ExampleView


    URLS = (
        ('/example', ExampleView, 'example_route'),
    )

The defined route ``/example`` is referring to the ``ExampleView`` class of the ``example_views.py`` file. This file can be accessed by going to the ``src/app/views``. Below you can find the content of the file:

::

    from flask_philo.views import BaseResourceView


    class ExampleView(BaseResourceView):
        def get(self):
            return self.json_response(
                status=200, data={'some_data': 'yes'})


Open the new Flask-Philo app in the browser
###########################################

If you don't have the server running in the browser, run the following command again:

::

    python3 manage.py runserver


Now, with the application running and with a route defined, if you open your favorite browser and type the following address you'll see the JSON code returned:

[http://localhost:8080/example]

The port 8080 should be the same displayed when you run the server:

::

    # Port 8080 in this case
    * Running on http://0.0.0.0:8080/ (Press CTRL+C to quit)
    * Restarting with stat
    * Debugger is active!
    * Debugger PIN: 147-416-135

The browser will show you, the response defined on the view file:

::

    {"some_data": "yes"}

You will also be able to check the status code of the http request (in the same window you started the server):

::

    * Running on http://0.0.0.0:8080/ (Press CTRL+C to quit)
    * Restarting with stat
    * Debugger is active!
    * Debugger PIN: 147-416-135
    127.0.0.1 - - [05/Dec/2017 00:06:01] "GET /example HTTP/1.1" 200 -


Running tests
#############

In order to run the test for the new app. You should run the following console command:

::

    python3 manage.py test


The return of the tests will be something like the print below:

::

    ===================================== test session starts ======================================
    platform darwin -- Python 3.5.1, pytest-3.3.0, py-1.5.2, pluggy-0.6.0
    rootdir: <where_your_project_is>/flask-philo-example/src, inifile:
    collected 1 item

    tests/test_views.py .                                                                    [100%]

    =================================== 1 passed in 0.02 seconds ===================================


The ``test_views.py`` file can be found in the ``src/tests`` folder.


Extending Flask-Philo projects
##############################

Flask-Philo projects are fully customizable and fully extensible. There are a lot of possible integrations. Below, you can see some examples and their documentation link:


- ORM Integration using Postgresql: [http://flask-philo.readthedocs.io/en/latest/db/postgresql-orm.html]
- AWS Integration [http://flask-philo.readthedocs.io/en/latest/cloud/aws/introduction.html]

In order to deploy a Flask-Philo application, we can use any tool we have in the market, here follows an example:

- NGINX and uWSGI for Flask-Philo app deployment: [http://flask-philo.readthedocs.io/en/latest/etc/flask_app_deploy.html]

For further information related to Flask-Philo, here follows the link for the documentation of the project:

[http://flask-philo.readthedocs.io/en/latest/index.html]

You can refer to the examples above, by checking our real Flask-Philo example in the following github project:

[https://github.com/Riffstation/flask-philo-example]


External Resources
------------------

- `Flask Website <http://flask.pocoo.org/>`_

- `Flask Book <http://flaskbook.com/>`_

- `SQL Alchemy <http://www.sqlalchemy.org/>`_

* `Python Redis <https://pypi.python.org/pypi/redis/2.10.3>`_

* `Python Elastic Search <https://www.elastic.co/guide/en/elasticsearch/client/python-api/current/index.html>`_
