Dependencies
============
TLP depends on (or conflicts with) the tools described below. They should be
implemented as package dependencies.

Package tlp
-----------
acpi-call - *optional*
     Kernel module needed for :doc:`/faq/battery` of Sandy Bridge and
     newer ThinkPads models (X220, T420 et al.).

.. include:: /include/no-package-dep.rst

awk, grep, sed - *mandatory*
    TLP is tested with the GNU version of these essential utilities.
    Your mileage with other implementations may vary.

.. include:: /include/busybox-not-supported.rst

ethtool - *optional*
    Used to disable Wake-on-LAN.

hdparm - *mandatory*
    Needed for hard disk advanced power management (APM) and to show information
    in :command:`tlp-stat -d`.

iw - *mandatory*
    Needed for Wi-Fi power save, replaces deprecated `iwconfig`
    (see wireless-tools below).

laptop-mode-tools - *conflicts*
    There can only be one power management tool at a time.

lsb-release - *optional* [before 1.4]
    Used to show distribution/release in :command:`tlp-stat -s`.

pciutils - *mandatory*
    Provides `lspci` used to show PCI(e) devices in :command:`tlp-stat -e`.

rfkill - *mandatory*
    Needed for switching radio devices on and off.

smartmontools - *optional*
    Provides `smartctl` used to show hard disk drive SMART data in
    :command:`tlp-stat -d`.

tp-smapi - *optional*
    Kernel modules needed to implement :doc:`/faq/battery` on older ThinkPads.

.. include:: /include/no-package-dep.rst

udev *- mandatory*
    Needed for event handling (see :doc:`architecture`) and providing `udevadm`.

usbutils - *mandatory*
    Provides `lsusb` used to show USB devices in :command:`tlp-stat -u`.

util-linux - *mandatory*
    Provides `flock` and `dmesg` (for :command:`tlp-stat -w`).

.. include:: /include/busybox-not-supported.rst

wireless-tools - *deprecated*
    Provides `iwconfig` for Wi-Fi power saving; only if `iw` and `rfkill`
    (see above) are not available.

x86_energy_perf_policy - *optional*
    Linux kernel version specific tool contained in the kernel tree
    (**tools/power/x86**). Needed to set the energy-performance bias (EPB)
    for Intel CPU's (kernel < 5.2 only).

.. note::

    Ubuntu provides it via the metapackage `linux-tools`, Debian via
    `linux-cpupower`. Your mileage with other distributions may vary.

Package tlp-rdw
---------------

tlp - *mandatory*
    Provides libraries **tlp-func-base** and **func.d/***.

network-manager - *mandatory*
    Used to hook ifup/ifdown events and to determine the corresponding
    interface type LAN/Wi-Fi/WWAN.
