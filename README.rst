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


Customizations
--------------
``IPYTHON_DIR``
    The Path to a custom ipython directory. default: ``None``

``AUTO_IMPORT_MODELS``
    Tries to autodetect django apps with models and imports them. default: ``True``

``IMPORT_MODULES``
    Defines additional modules that should be imported.
    Should be a tuple or list containing entries like (module, imports).
    Examples::

        DJANGO_SH_IMPORT_MODULES = (
            ('datetime', ('datetime', 'timedelta')),  # -> from datetime import datetime, timedelta
            ('re', None),                             # -> import re
            ('decimal', 'Decimal'),                   # -> from decimal import Decimal
            ('foo.bar', '*')                          # -> from foo.bar import *
        )

    default: ``()``

``HOOK_ADD_ARGUMENTS``
    A function that adds arguments to the `sh` command. Example::

        def DJANGO_SH_HOOK_ADD_ARGUMENTS(parser: CommandParser) -> None:
            parser.add_argument(...)

    default: ``None``

``HOOK_GET_IMPORTED_OBJECTS``
    A function that is called after importing models and modules.
    Can be used to further extend the `imported_objects` name space or to check command arguments. Example::

        def DJANGO_SH_HOOK_GET_IMPORTED_OBJECTS(imported_objects: dict, options: dict) -> None:
            multiplier = int(options.get('multiplier', 0))
            imported_objects['multiply'] = lambda x: x * multiplier

    default: ``None``

``HOOK_MODIFY_COMMAND``
    Can be used to alter the command provided to ``python manage.py sh -c '<command>'`` Example::

        def DJANGO_SH_HOOK_MODIFY_COMMAND(command: str) -> str:
            return f'start=time.time()\\n{command}\\nprint("Command took", time.time() - start, "seconds")'

    default: ``None``

