galicaster-plugin-blinkstick
============================

Adding much needed flashing lights to Galicaster_!

This plugin allows you to use a BlinkStick_ to alert people in the room of the
current recording status of the Galicaster.

Specifically, we are using `BlinkStick Square`_ with the enclosure, though this
might work for the other blinkstick hardware too. It might also be a good
starting point for other lights.

By default the light will turn yellow when a recording is upcoming (starting
in less than a minute), red when recording, and flash red when paused. This
can be configured using the settings described below.

Usage
-----

Install using ``sudo pip2 install .`` in this directory. The official
``blinkstick`` python module is required, and should be installed automatically
by pip as needed.

You can also install manually by copying ``galicaster_plugin_blinkstick/`` into
the Galicaster plugins directory, renaming it as ``blinkstick`` and then
installing the blinkstick module with ``sudo pip2 install blinkstick``.

Either way, you should add a udev rule to make sure ordinary users can access
it using ``sudo blinkstick --add-udev-rule``. or you can manually achieve the
same thing with:

::

  echo "SUBSYSTEM==\"usb\", ATTR{idVendor}==\"20a0\", ATTR{idProduct}==\"41e5\", MODE:=\"0666\"" | sudo tee /etc/udev/rules.d/85-blinkstick.rules

Add the following to your ``conf.ini`` file:

::

    [plugins]
    blinkstick = True

    [blinkstick]
    preview_color = #00ff00
    rec_color = #ff0000
    pause_color = #ff0000
    pause_delay = 1000
    upcoming_color = #ffff00
    error_color = #ffbf00

Settings
--------

+----------------+---------+----------------------------------------------------+--------------------+
| Setting        | Type    | Description                                        | Default            |
+================+=========+====================================================+====================+
| preview_color  | string  | Hex string representing preview color              | '#00ff00' (Green)  |
+----------------+---------+----------------------------------------------------+--------------------+
| rec_color      | string  | Hex string representing record color               | '#ff0000' (Red)    |
+----------------+---------+----------------------------------------------------+--------------------+
| pause_color    | string  | Hex string representing pause color                | '#ff0000' (Red)    |
+----------------+---------+----------------------------------------------------+--------------------+
| pause_delay    | integer | Number of milliseconds between flashes when paused | 1000 (1 second)    |
+----------------+---------+----------------------------------------------------+--------------------+
| upcoming_color | string  | Hex string representing upcoming color. This       | '#ffff00' (Yellow) |
|                |         | color is used when a recording is about to start   |                    |
+----------------+---------+----------------------------------------------------+--------------------+
| error_color    | string  | Hex string representing error color                | '#ffbf00' (Orange) |
+----------------+---------+----------------------------------------------------+--------------------+

Source
------
Source code is available at https://github.com/ppettit/galicaster-plugin-blinkstick

.. _Galicaster: https://github.com/teltek/Galicaster
.. _BlinkStick: https://www.blinkstick.com/
.. _BlinkStick Square: https://www.blinkstick.com/products/blinkstick-square
