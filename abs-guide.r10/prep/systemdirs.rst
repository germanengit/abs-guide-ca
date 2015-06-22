.. raw:: html

   <div class="NAVHEADER">

.. raw:: html

   <table border="0" cellpadding="0" cellspacing="0" summary="Header navigation table" width="100%">

.. raw:: html

   <tr>

.. raw:: html

   <th align="center" colspan="3">

Advanced Bash-Scripting Guide:

.. raw:: html

   </th>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td align="left" valign="bottom" width="10%">

`Prev <files.html>`__

.. raw:: html

   </td>

.. raw:: html

   <td align="center" valign="bottom" width="80%">

.. raw:: html

   </td>

.. raw:: html

   <td align="right" valign="bottom" width="10%">

`Next <tabexpansion.html>`__

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

--------------

.. raw:: html

   </div>

.. raw:: html

   <div class="APPENDIX">

  Appendix I. Important System Directories
=========================================

Sysadmins and anyone else writing administrative scripts should be
intimately familiar with the following system directories.

-  ``        /bin       ``

   Binaries (executables). Basic system programs and utilities (such as
   **bash** ).

-  ``        /usr/bin       `` ` [1]  <systemdirs.html#FTN.AEN23969>`__

   More system binaries.

-  ``        /usr/local/bin       ``

   Miscellaneous binaries local to the particular machine.

-  ``        /sbin       ``

   System binaries. Basic system administrative programs and utilities
   (such as **fsck** ).

-  ``        /usr/sbin       ``

   More system administrative programs and utilities.

-  ``        /etc       ``

   *Et cetera* . Systemwide configuration scripts.

   Of particular interest are the
   ```         /etc/fstab        `` <system.html#FSTABREF>`__
   (filesystem table), ``        /etc/mtab       `` (mounted filesystem
   table), and the
   ```         /etc/inittab        `` <system.html#INITTABREF>`__ files.

-  ``        /etc/rc.d       ``

   Boot scripts, on Red Hat and derivative distributions of Linux.

-  ``        /usr/share/doc       ``

   Documentation for installed packages.

-  ``        /usr/man       ``

   The systemwide `manpages <basic.html#MANREF>`__ .

-  ``        /dev       ``

   Device directory. Entries (but *not* mount points) for physical and
   virtual devices. See `Chapter 29 <devproc.html>`__ .

-  ``        /proc       ``

   Process directory. Contains information and statistics about running
   processes and kernel parameters. See `Chapter 29 <devproc.html>`__ .

-  ``        /sys       ``

   Systemwide device directory. Contains information and statistics
   about device and device names. This is newly added to Linux with the
   2.6.X kernels.

-  ``        /mnt       ``

   *Mount* . Directory for mounting hard drive partitions, such as
   ``        /mnt/dos       `` , and physical devices. In newer Linux
   distros, the ``        /media       `` directory has taken over as
   the preferred mount point for I/O devices.

-  ``        /media       ``

   In newer Linux distros, the preferred mount point for I/O devices,
   such as CD/DVD drives or USB flash drives.

-  ``        /var       ``

   *Variable* (changeable) system files. This is a catchall "scratchpad"
   directory for data generated while a Linux/UNIX machine is running.

-  ``        /var/log       ``

   Systemwide log files.

-  ``        /var/spool/mail       ``

   User mail spool.

-  ``        /lib       ``

   Systemwide library files.

-  ``        /usr/lib       ``

   More systemwide library files.

-  ``        /tmp       ``

   System temporary files.

-  ``        /boot       ``

   System *boot* directory. The kernel, module links, system map, and
   boot manager reside here.

   .. raw:: html

      <div class="WARNING">

   +--------------------------------------+--------------------------------------+
   | |Warning|                            |
   | Altering files in this directory may |
   | result in an unbootable system.      |
   +--------------------------------------+--------------------------------------+

   .. raw:: html

      </div>

.. raw:: html

   </div>

Notes
~~~~~

+--------------------------+--------------------------+--------------------------+
| ` [1]                    |
|  <systemdirs.html#AEN239 |
| 69>`__                   |
| Some early UNIX systems  |
| had a fast,              |
| small-capacity fixed     |
| disk (containing         |
| ``        /       `` ,   |
| the root partition), and |
| a second drive which was |
| larger, but slower       |
| (containing              |
| ``        /usr       ``  |
| and other partitions).   |
| The most frequently used |
| programs and utilities   |
| therefore resided on the |
| small-but-fast drive, in |
| ``        /bin       ``  |
| , and the others on the  |
| slower drive, in         |
| ``        /usr/bin       |
|  ``                      |
| .                        |
|                          |
| This likewise accounts   |
| for the split between    |
| ``        /sbin       `` |
| and                      |
| ``        /usr/sbin      |
|   ``                     |
| ,                        |
| ``        /lib       ``  |
| and                      |
| ``        /usr/lib       |
|  ``                      |
| , etc.                   |
+--------------------------+--------------------------+--------------------------+

.. raw:: html

   <div class="NAVFOOTER">

--------------

.. raw:: html

   <table border="0" cellpadding="0" cellspacing="0" summary="Footer navigation table" width="100%">

.. raw:: html

   <tr>

.. raw:: html

   <td align="left" valign="top" width="33%">

`Prev <files.html>`__

.. raw:: html

   </td>

.. raw:: html

   <td align="center" valign="top" width="34%">

`Home <index.html>`__

.. raw:: html

   </td>

.. raw:: html

   <td align="right" valign="top" width="33%">

`Next <tabexpansion.html>`__

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td align="left" valign="top" width="33%">

Important Files

.. raw:: html

   </td>

.. raw:: html

   <td align="center" valign="top" width="34%">

.. raw:: html

   </td>

.. raw:: html

   <td align="right" valign="top" width="33%">

An Introduction to Programmable Completion

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

.. raw:: html

   </div>

.. |Warning| image:: ../images/warning.gif
