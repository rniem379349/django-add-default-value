Django Add Default Value
========================

Django Migration Operation that can be used to transfer a field's default value
to the database scheme.

[![PyPi](https://img.shields.io/pypi/v/django-add-default-value.svg?branch=master)](https://pypi.python.org/pypi/django-add-default-value/)
[![License](https://img.shields.io/github/license/3yourmind/django-add-default-value.svg)](./LICENSE)
[![Contributing](https://img.shields.io/badge/PR-welcome-green.svg)](https://github.com/3YOURMIND/django-add-default-value/pulls)
[![3yourminD-Careers](https://img.shields.io/badge/3YOURMIND-Hiring-brightgreen.svg)](https://www.3yourmind.com/career)
[![Stars](https://img.shields.io/github/stars/3YOURMIND/django-add-default-value.svg?style=social&label=Stars)](https://github.com/3YOURMIND/django-add-default-value/stargazers)


Supported Databases
------------

* MySQL (or compatible)
* PostgreSQL
* MSSQL (currently not tested)

Installation
------------
`pip install django-add-default-value`

You can then use ``AddDefaultValue`` in your migration file to transfer the default
values to your database. Afterwards, it's just the usual ``./manage.py migrate``.

Usage
-----

Add this manually to a autogenerated Migration, that adds a new field::

    AddDefaultValue(
        model_name='my_model',
        name='my_field',
        value='my_default'
    )


### Example

Given the following migration::

    operations = [
        migrations.AddField(
            field=models.CharField(default='my_default', max_length=255),
            model_name='my_model',
            name='my_field',
        ),
    ]

Modify the migration to add a default value::


    +from django_add_default_value import AddDefaultValue
    +
     operations = [
         migrations.AddField(
             field=models.CharField(default='my_default', max_length=255),
             model_name='my_model',
             name='my_field',
         ),
    +    AddDefaultValue(
    +        model_name='my_model',
    +        name='my_field',
    +        value='my_default'
    +    )
     ]

If you check ``python manage.py sqlmigrate [app name] [migration]``,
you will see that the default value now gets set.

Contributing
------------

First of all, thank you very much for contributing to this project. Please base
your work on the ``master`` branch and target ``master`` in your pull request.

To succesfully use the `dbshell` management command (very useful for debugging),
the client binaries for the respective database engines are needed.

Then install [pipenv](https://pipenv.readthedocs.io/en/latest/install/#installing-pipenv).
Edit the `Pipfile` to select your Django version and the accompanying MS-SQL
driver. Make sure you don't commit this change in any pull request - we always
set it to the oldest supported version.

Once you've updated the Pipfile, run `pipenv install --python 3 --dev`. You
should now have a working development environment as a virtualenv. To access it,
run `pipenv shell` or prefix commands with `pipenv run`. For more information
see the [pipenv documentation](https://pipenv.readthedocs.io/en/latest/basics/).

### Testing
Copy the relevant sample settings file in `test_project` to the file without
 `.sample` in it. Adjust the values to match your environment (or match your
environment to the values).

You should now be able to run the tests using `tox`. Select your environment
when needed, using the `-e` command line flag. See
[Tox's excellent documentation](https://preview.tinyurl.com/y3faq6ab).


License
-------

``django-add-default-value`` is released under the Apache 2.0 License.


