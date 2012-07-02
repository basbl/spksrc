spksrc
======
spksrc is a cross compilation framework intended to compile and package softwares for Synology NAS

Requirements
------------
To use spksrc, it is recommended to use a virtual machine with Debian stable OS installed. You'll also
need some stuff::

    sudo aptitude install build-essential debootstrap python-pip automake libgmp-dev libltdl-dev libunistring-dev libffi-dev ncurses-dev

You are now ready to use spksrc and make almost all SPKs. If you have any problem, try installing the
missing packages on your virtual machine.

Usage
-----
Lets start with an example::

    git clone https://github.com/SynoCommunity/spksrc.git
    cd spksrc/spk/transmission
    make arch-88f6281

What have I done?
^^^^^^^^^^^^^^^^^

* You cloned the repository
* Went into the directory of the SPK for transmission
* Started building the SPK for the architecture 88f6281 (see the `list of architectures`_)

At the end of the process, the SPK will be available in ``spksrc/packages/``

What is spksrc doing?
^^^^^^^^^^^^^^^^^^^^^

* First spksrc will read ``spksrc/spk/transmission/Makefile``
* Download the adequate toolchain for the chosen architecture
* Recursivly:

  * Process dependencies if any
  * Download the source in ``spksrc/distrib/``
  * Extract the source
  * ``configure``
  * ``make``
  * ``make install``

* Package all the requirements into a SPK under ``spksrc/packages/``:

  * Binaries
  * Installer script
  * Start/Stop/Status script
  * Package icon
  * Wizards (optional)
  * Help files (optional)

Contribute
----------
The only thing you should be editing in spksrc is Makefiles. To make a SPK, start by cross-compiling
the underlying package. To do so:

* Copy a standard cross package like ``spksrc/cross/transmission/Makefile``
  in your new package directory ``spksrc/cross/newpackage/``
* Edit the Makefile variables so it fits your new package
* Empty variables ``DEPENDS`` and ``CONFIGURE_ARGS`` in the Makefile
* Try to cross-compile and fix issues as they come (missing dependencies, configure arguments, patches)

  * ``cd spksrc/cross/newpackage/``
  * ``make arch-88f6281``
  * Use ``make clean`` to clean up the whole working directory after a failed attempt
  
* On a successful cross-compilation create a PLIST file with the same syntax as
  ``spksrc/cross/transmission/PLIST`` but based on the auto-generated PLIST for your
  new package at ``spksrc/cross/newpackage/work-88f6281/newpackage.plist``

Once you have successfully cross compiled the new package, to create the SPK:

* Copy a standard SPK directory like ``spksrc/spk/transmission``
  in your new SPK directory ``spksrc/spk/newspk``
* Edit the stuff to fit your needs

After all that hard work, submit a pull request to have your work merged with the main repository
on GitHub and published in `SynoCommunity's repository`_.

If you are not familiar with git or GitHub, please refer to the excellent `GitHub help pages`_.

Donate
------
If you like spksrc and packages made out of it, please consider making a donation to his authors:

* Diaoul

  .. image:: https://www.paypal.com/en_US/i/btn/btn_donate_LG.gif
    :target: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=F6GDE5APQ4SBN

  .. image:: http://api.flattr.com/button/flattr-badge-large.png
    :target: http://flattr.com/thing/718012/SynoCommunity

Bugs
----
If you find a bug please report it in the `bug tracker`_ if it has not already been reported. Be sure to provide as much information as possible.

License
-------
When not explicitly set, files are placed under a `3 clause BSD license`_


.. _list of architectures: http://forum.synology.com/wiki/index.php/What_kind_of_CPU_does_my_NAS_have
.. _3 clause BSD license: http://www.opensource.org/licenses/BSD-3-Clause
.. _bug tracker: https://github.com/SynoCommunity/spksrc/issues
.. _GitHub help pages: https://help.github.com
.. _SynoCommunity's repository: http://www.synocommunity.com/