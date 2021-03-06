Installing MPF on Mac
=====================

MPF can be used on Mac OS X 10.9 and newer, including Mavericks, Yosemite,
El Capitan, and MacOS Sierra.

.. note::

   MPF cannot run in a Mac virtual machine (like in VMware Fusion or Parallels)
   if the guest OS is Mac, though running MPF in a Windows or Linux VM on a
   Mac is fine.

Also at this time, installing all the components you need to run MPF on a Mac
will require almost 2 GB of disk space. MPF itself it only about 12 MB, but
there are a lot of supporting things that MPF needs as you'll see here.

We have a video which shows this entire installation process in action
which is available at `<https://www.youtube.com/watch?v=lJEfQGffXsA>`_

Here are the steps to install MPF on a Mac:

Step 0. Uninstall your previous MPF app installation
----------------------------------------------------

The process for running MPF on a Mac has changed as of Jan 10, 2017.
Previously we had an MPF.app that you downloaded which contained Python and
everything you needed.

If you used MPF on a Mac prior to this and you have the MPF.app, you need to
remove it first. If you have never installed MPF on your Mac before, then
proceed directly to Step 1 below.

To remove the old MPF Mac installation:

1. Delete the "MPF.app" from your Applications folder.
2. Delete the "mpf" alias in ``/usr/local/bin``.
3. Delete the "kivy" alias in ``/usr/local/bin``.

If you don't know how to find your ``/usr/local/bin`` folder, you can use
the "Go to Folder" technique shown in Step 1.

1. Download the Mac Multimedia Frameworks
-----------------------------------------

MPF uses open source multimedia frameworks called GStreamer and SDL2 for its
graphics, video, and sound features. So next you need to download these
frameworks and copy them to your Mac's frameworks folder. There are actually
five different frameworks MPF needs, and downloading them all separately is
kind of a pain (especially finding the right versions and everything), so we
have created a single ZIP file which has everything you need.

Download the zip of the multimedia frameworks `here <https://mpf.kantert.net/mpf_mac_frameworks.zip>`_.
(Thanks to MPF developer Jan Kantert for hosting it!) The zipped download is 170 MB,
and the unzipped size is 529 MB.

Unzip it, and copy (or drag and drop) the five things in the zip file's
``Frameworks`` folder to your own Mac's ``/Library/Frameworks`` folder.

Depending on your Mac's settings, you might not see the ``/Library/Frameworks``
folder in Finder. If this is the case, use the *Go -> Go to Folder...* menu,
and then type "/Library/Frameworks" and hit enter.

The following three images illustrate the steps:

.. image:: images/mac_finder_go_to_folder.jpg

.. image:: images/mac_finder_go_to_folder2.jpg

Note that you will need to authenticate (which just means you have to enter
your password) in order to be able to copy those frameworks into your Mac's
frameworks folder. The authentication message will automatically pop up when
you drag and drop the files:

.. image:: images/mac_copy_frameworks.jpg

When you're done, your Mac's ``/Library/Frameworks`` folder should have
the five new frameworks (plus whatever random ones you already had), which
should look something like this:

.. image:: images/mac_frameworks_copied.jpg

2. Install the Mac developer tools
----------------------------------

Next you have to install something called the "Command Line Developer Tools"
which is a package of software development tools created by Apple which MPF
relies on to get installed.

To do this, you need to use the "Terminal" app (which is essentially a
command prompt window for the Mac).

The easiest way to launch the Terminal app is to use Spotlight (press the
CMD + Spacebar) and then just type "Terminal", like this:

.. image:: images/mac_spotlight_terminal.jpg

Next, type the following command into the prompt in the terminal and press
Enter:

::

   xcode-select --install

That should pop up a box which gives you the option to install the command
line tools, like this:

.. image:: images/mac_install_command_line_tools.jpg

Click the "Install" button here to get just the command line tools. The
"Get XCode" button installs more than you need.

The download will be about 150 MB, and the total install will be about 1.1 GB.

If you already have the command line tools installed, that's fine. You'll get
some kind of error saying they're already installed and you can move on.

3. Install Python 3.5 (not Python 3.6)
--------------------------------------

MPF is written in a computer language called "Python". This means you have to install Python
first before you can use MPF. Luckily this is just a one-time install, and you don't have to
install it again if you update MPF later.

On Mac platforms, MPF requires Python 3.4 or 3.5. (There is a Python 3.6, but
that's untested with MPF.) So we recommend that you install Python 3.5.

You can download Python 3.5 directly via `this link <https://www.python.org/ftp/python/3.5.2/python-3.5.2-macosx10.6.pkg>`_.
(Note that the final digit in the Python version number is the "patch" number,
so 3.5.2 is the latest version of Python 3.5.)

.. image:: images/mac_install_python_1.jpg

Installing Python is pretty straightforward. It's a standard Mac installation
package. You can click next, next, next, agree to the license, enter your
password, and you're all set.

.. note::

   Macs have an older version of Python built in, but it's Python 2.x, and MPF
   requires Python 3, so that's why you have to install Python now. The new
   Python 3 that you install here will happily live alongside the Python 2.x
   that your Mac already has.

You can check to make sure Python 3.5 installed correctly from the Terminal
window. To do that, run the command:

::

   python3 --version

You should see it print something like "Python 3.5.2". Note that you have
to run the command "Python3", not "Python", since the regular python command
without the "3" on the end points to the Python 2.x that's built into your
Mac. Here's a screenshot showing running "python" and "python3" and the
different between the two:

.. image:: images/mac_python_versions.jpg

4. Install/upgrade some Python components
-----------------------------------------

Python includes a utility called "pip" which is the name of the Python Package
Manager. Pip is used to install Python packages and applications from
the web. (It's kind of like an app store for Python apps.)

So the next step is to use pip to install/upgrade some components that we'll
need to install MPF. (This command will actually update pip itself too.)

Note that the command you run is "pip3", not "pip", since again we need to
point to the pip that's associated with the Python 3.5 installation, not the
built-in 2.x version.

So next run the following command:

::

    pip3 install pip setuptools cython==0.24.1 --upgrade

This command will download and install the latest versions of the *pip* and
*setuptools* packages, as well as version 0.24.1 of a package called *cython*.
The results will look something like this (though the exact version numbers
might be different depending on what's the latest whenever you're running this):

::

   Collecting pip
     Downloading pip-9.0.1-py2.py3-none-any.whl (1.3MB)
       100% |################################| 1.3MB 2.5MB/s
   Collecting setuptools
     Downloading setuptools-32.3.1-py2.py3-none-any.whl (479kB)
       100% |################################| 481kB 4.3MB/s
   Collecting cython==0.24.1
     Downloading Cython-0.24.1-cp35-cp35m-macosx_10_6_intel.macosx_10_9_intel.macosx_10_9_x86_64.macosx_10_10_intel.macosx_10_10_x86_64.whl (3.8MB)
       100% |################################| 3.8MB 7.6MB/s
   Installing collected packages: pip, setuptools, cython
   Successfully installed cython-0.24.1 pip-9.0.1 setuptools-32.3.1

5. Install MPF
--------------

Next you can run pip again to install MPF itself. Technically what you're
installing is "mpf-mc", which is the
`Mission Pinball Framework Media Controller <http://docs.missionpinball.org/en/latest/start/media_controller.html>`_
package, but that package will also install the MPF game engine. Install MPF
like this:

::

   pip3 install mpf-mc

Your results should look something like the results below. The MPF install will
download and install several other packages which what all these other things
are.

.. note::

   The "kivy" component will take awhile to install. Maybe a minute or two
   where it looks like it's not doing anything, but it's fine.

::

   Brians-Mac:~ brian$ pip3 install mpf-mc
   Collecting mpf-mc
     Downloading mpf-mc-0.32.12.tar.gz (11.1MB)
       100% |################################| 11.1MB 29.6MB/s
   Collecting ruamel.yaml<0.11,>=0.10 (from mpf-mc)
     Downloading ruamel.yaml-0.10.23.tar.gz (228kB)
       100% |################################| 235kB 9.0MB/s
   Collecting mpf>=0.32.6 (from mpf-mc)
     Downloading mpf-0.32.6.tar.gz (556kB)
       100% |################################| 563kB 18.0MB/s
   Collecting kivy>=1.9.1 (from mpf-mc)
     Downloading kivy-1.9.1.tar.gz (16.4MB)
       100% |################################| 16.4MB 7.4MB/s
   Collecting ruamel.base>=1.0.0 (from ruamel.yaml<0.11,>=0.10->mpf-mc)
     Downloading ruamel.base-1.0.0-py3-none-any.whl
   Collecting pyserial>=3.2.0 (from mpf>=0.32.6->mpf-mc)
     Downloading pyserial-3.2.1-py2.py3-none-any.whl (189kB)
       100% |################################| 194kB 4.1MB/s
   Collecting pyserial-asyncio>=0.2 (from mpf>=0.32.6->mpf-mc)
     Downloading pyserial_asyncio-0.3-py3-none-any.whl
   Collecting Kivy-Garden>=0.1.4 (from kivy>=1.9.1->mpf-mc)
     Downloading kivy-garden-0.1.4.tar.gz
   Collecting requests (from Kivy-Garden>=0.1.4->kivy>=1.9.1->mpf-mc)
     Downloading requests-2.12.4-py2.py3-none-any.whl (576kB)
       100% |################################| 583kB 4.8MB/s
   Installing collected packages: ruamel.base, ruamel.yaml, pyserial, pyserial-asyncio, mpf, requests, Kivy-Garden, kivy, mpf-mc
     Running setup.py install for ruamel.yaml ... done
     Running setup.py install for mpf ... done
     Running setup.py install for Kivy-Garden ... done
     Running setup.py install for kivy ... done
     Running setup.py install for mpf-mc ... done
   Successfully installed Kivy-Garden-0.1.4 kivy-1.9.1 mpf-0.32.6 mpf-mc-0.32.12 pyserial-3.2.1 pyserial-asyncio-0.3 requests-2.12.4 ruamel.base-1.0.0 ruamel.yaml-0.10.23
   Brians-Mac:~ brian$

If you want to make sure that MPF was installed, quit the Terminal app and restart it, and then run:

::

   mpf --version

This command can be run from anywhere and should produce output something like
this:

::

   Brians-Mac:~ brian$ mpf --version
   MPF v0.33.12

(Note that the actual version number of your MPF installation will be whatever
version is the latest.)

6. Download & run the "Demo Man" example game
---------------------------------------------

Now that you have MPF installed, you probably want to see it in action. The easiest way to do that is
to download a bundle of MPF examples and run our "Demo Man" example game. To do that, follow
the instructions in the :doc:`/example_games/demo_man` guide.

There's another example project you can also check out if you want called the "MC Demo" (for media controller demo)
that lets you step through a bunch of example display things (slides, widgets, sounds, videos, etc).
Instructions for running the MC Demo are :doc:`here </example_games/mc_demo>`.

7. Install whatever drivers your hardware controller needs
----------------------------------------------------------

If you're using MPF with a physical machine, then there will be some specific
steps you'll need to take to get the drivers installed and configured for
whatever control system you've chosen. See the :doc:`control systems </hardware/index>`
documentation for details. (You don't have to worry about that now if you just
want to play with MPF first.)

Running MPF
-----------

See the section :doc:`/running/index` for details and command-line options.

Keeping MPF up-to-date
----------------------

Since MPF is a work-in-progress, you can use the *pip* command to update your
MPF installation.

To to this, run the following:

::

  pip3 install mpf mpf-mc --upgrade

This will cause *pip* to contact PyPI to see if there's a newer version of the
MPF MC (and any of its requirements, like MPF). If newer versions are found, it
will download and install them.

Next steps!
-----------

Now that MPF is installed, you can follow our
:doc:`step-by-step tutorial </tutorial/index>` which will show you how to start
building your own game in MPF!
