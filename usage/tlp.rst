tlp
---
.. topic:: Purpose

    Apply TLP's settings and change mode of operation.

Start or restart TLP
^^^^^^^^^^^^^^^^^^^^
Apply all configured settings according to the actual power source: ::

    sudo tlp start

.. note:: Also use this command to apply changes after editing the configuration.

Battery Mode
^^^^^^^^^^^^
Apply the battery settings profile and enter manual mode: ::

    sudo tlp bat

Hint: manual mode means that changes to the power source will be ignored until
the next reboot or :command:`tlp start` is issued to resume automatic mode.

AC Mode
^^^^^^^
Apply the AC settings profile and enter manual mode: ::

    sudo tlp ac

Hint: manual mode means that changes to the power source will be ignored until
the next reboot or :command:`tlp start` is issued to resume automatic mode.

USB Autosuspend
^^^^^^^^^^^^^^^
Apply autosuspend mode for all attached USB devices except input and blacklisted
devices: ::

    sudo tlp usb

Optical Drive
^^^^^^^^^^^^^
Power off optical drive in MediaBay or Ultrabay: ::

    sudo tlp bayoff

Hints:

* Re-power the drive by releasing and reinserting the drive slot/Ultrabay eject lever; on newer models push the media eject button
* Devices other than optical drives – in particular hard disk drives – are not affected by this command

.. _cmd-tlp-battery-features:

Battery Features
^^^^^^^^^^^^^^^^
.. include:: ../include/expl-battery-features.rst
.. include:: ../include/disc-battery-features.rst


Change battery charge thresholds to temporary values
""""""""""""""""""""""""""""""""""""""""""""""""""""
::

    sudo tlp setcharge [ START_THRESH STOP_THRESH [ BAT0 | BAT1 ] ]

Sets the thresholds to the given values. Valid thresholds range from 1 to 100;
`START_THRESH` must be below `STOP_THRESH` - 3. Without parameters the configured
settings for the main battery (BAT0) are applied. Upon reboot, thresholds are
reset to the configured settings.

Example: ::

    sudo tlp setcharge 70 90 BAT0

Applies thresholds of 70/90% to the main battery (BAT0).

.. note::

    :command:`tlp setcharge` changes the thresholds only temporarily. To make the
    change permanent, you must activate or change the related settings in the
    configuration file. Refer to :doc:`/settings/battery`.

Charge battery to full capacity
"""""""""""""""""""""""""""""""
::

    sudo tlp fullcharge [ BAT0 | BAT1 ]

Applies factory settings i.e. thresholds 96/100% to initiate the charge. Upon
reboot, thresholds are reset to the configured settings.

Hint: after setting the thresholds the command terminates; it does not wait for
the charge to complete.

Example: ::

    sudo tlp fullcharge BAT1

Charges the auxiliary battery (BAT1) to full capacity.

Charge battery once to the upper charge threshold
"""""""""""""""""""""""""""""""""""""""""""""""""
::

     sudo tlp chargeonce [ BAT0 | BAT1 ]

Sets the lower threshold to upper threshold - 4 to initiate the charge.
Upon reboot, thresholds are reset to the configured settings.

Hint: after setting he thresholds the command terminates; it does not wait for
the charge to complete.

Discharge battery on AC power
"""""""""""""""""""""""""""""
::

    sudo tlp discharge [ BAT0 | BAT1 ]

BAT0 selects the main battery, BAT1 the auxiliary/Ultrabay battery for discharge.
The command continously shows remaining capacity and estimated discharge time.
Discharging may be stopped at any time with :kbd:`Control-C`.

Hints:

* The command terminates automatically when the battery is discharged completely
* The command needs the AC power supply plugged in
* Normal use of the ThinkPad is possible during the discharge process
* ThinkPads with two batteries: the battery controller can only handle one
  battery at a time; while discharging one battery with this command the other
  battery can neither be charged nor discharged
* When encountering problems, see the FAQ: :doc:`/faq/battery`

Recalibrate battery on AC power
"""""""""""""""""""""""""""""""
::

    sudo tlp recalibrate [ BAT0 | BAT1 ]

This command works as follows:

* Resets the charge thresholds to factory defaults 96/100 %
* Discharges the selected battery completely (see description of
  :command:`tlp discharge` above)
* When discharging is complete the command terminates; it does not wait for the
  charge to complete
* Important: to complete the recalibration process, let the battery charge to
  100 % subsequently (you may power off but not remove AC power)

Example: ::

    sudo tlp recalibrate BAT0

Recalibrates the main battery (BAT0).

Hints:

* ThinkPads with two batteries: the battery controller can only handle one
  battery at a time; while discharging one battery with this command the other
  battery can neither be charged nor discharged
* Recalibration forces the battery pack to update the `energy_full` or
  `charge_full` information shown by :command:`tlp-stat -b`
* Recalibration does not repair defective or worn out batteries

Disk IDs
^^^^^^^^
::

    tlp diskid

Shows the IDs of all attached disk drives.
