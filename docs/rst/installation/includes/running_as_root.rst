.. note::

    When running the *DDS Monitor* as ``root`` (e.g. inside a Docker container), the application may fail to start
    with a ``Running as root without --no-sandbox is not supported`` error.
    To fix it, export the following variable before launching it:

    .. code-block:: bash

        export QTWEBENGINE_CHROMIUM_FLAGS="--no-sandbox"
