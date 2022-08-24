=========
Django-sh
=========

Provides a ``sh`` management-command that can be customizable via django settings.

Quick start
-----------
1. Install with ``pip install git+https://gitlab.com/software-design-public/django-sh.git``

2. Add "sh" to your INSTALLED_APPS setting like this::

    INSTALLED_APPS = [
        ...
        'sh',
    ]

3. Have a look at sh/settings.py for available customizations

4. Override any of the settings in your project's settings.py, prepending the names with ``DJANGO_SH_``

5. Start the shell via ``python manage.py sh``
