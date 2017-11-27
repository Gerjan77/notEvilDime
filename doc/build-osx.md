Mac OS X Build Instructions and Notes
====================================
This guide will show you how to build notevildimed(headless client) for OSX.

Notes
-----

* See [readme-qt.md](readme-qt.md) for instructions on building notEvilDime-Qt, the
graphical user interface.
* Tested on OS X 10.5 through 10.8 on Intel processors only. PPC is not
supported because it is big-endian.
* All of the commands should be executed in a Terminal application. The
built-in one is located in `/Applications/Utilities`.

Preparation
-----------

You need to install XCode with all the options checked so that the compiler
and everything is available in /usr not just /Developer. XCode should be
available on your OS X installation media, but if not, you can get the
current version from https://developer.apple.com/xcode/. If you install
Xcode 4.3 or later, you'll need to install its command line tools. This can
be done in `Xcode > Preferences > Downloads > Components` and generally must
be re-done or updated every time Xcode is updated.

There's an assumption that you already have `git` installed, as well. If
not, it's the path of least resistance to install [Github for Mac](https://mac.github.com/)
(OS X 10.7+) or
[Git for OS X](https://code.google.com/p/git-osx-installer/). It is also
available via Homebrew or MacPorts.

You will also need to install [Homebrew](http://mxcl.github.io/homebrew/)
AND [MacPorts](https://www.macports.org/) in order to install library
dependencies. It's largely a religious decision which to choose, but, as of
December 2012, MacPorts is a little easier because you can just install the
dependencies immediately - no other work required. If you're unsure, read
the instructions through first in order to assess what you want to do.
Homebrew is a little more popular among those newer to OS X.

The installation of the actual dependencies is covered in the Instructions
sections below.

Compiler:

    brew search gcc
    brew unlink gcc
    brew install gcc@4.9
    brew install boost
    
Require the following specific versions of dependencies:
    
    brew install openssl@1.1
    sudo port install db48@+no_java
    
Check the versions:

     brew ls --versions
     
berkeley-db@4 4.8.30
gcc@4.9 4.9.4
openssl@1.1 1.1.0g
boost@1.65.1



MiniUPnPc: We require specifically version 1.6
-------
To install the library and headers on the system use :

    cd dependencies/miniupnpc-1.6
    sudo su
    INSTALLPREFIX=/opt/local make install
    exit

upnpc.c is a sample client using the libminiupnpc.
To use the libminiupnpc in your application, link it with
libminiupnpc.a (or .so) and use the following functions found in miniupnpc.h,
upnpcommands.h and miniwget.h :
- upnpDiscover()
- miniwget()
- parserootdesc()
- GetUPNPUrls()
- UPNP_* (calling UPNP methods)

Note : use #include <miniupnpc/miniupnpc.h> etc... for the includes
and -lminiupnpc for the link



       sudo port install db48@+no_java


Building the Deamon `notEvilDimed`
-------

1. Clone the github tree to get the source code and go into the directory.

        git clone https://github.com/Gerjan77/notEvilDime
        cd notEvilDime

2.  Build notevildimed:

        cd src
        make -f makefile.osx

3.  It is a good idea to build and run the unit tests, too:

        make -f makefile.osx test


Creating a release build
------------------------

A notevildimed binary is not included in the notEvilDime-Qt.app bundle. You can ignore
this section if you are building `notevildimed` for your own use.

If you are building `notevildimed` for others, your build machine should be set up
as follows for maximum compatibility:

All dependencies should be compiled with these flags:

    -mmacosx-version-min=10.5 -arch i386 -isysroot /Developer/SDKs/MacOSX10.5.sdk

For MacPorts, that means editing your macports.conf and setting
`macosx_deployment_target` and `build_arch`:

    macosx_deployment_target=10.5
    build_arch=i386

... and then uninstalling and re-installing, or simply rebuilding, all ports.

As of December 2012, the `boost` port does not obey `macosx_deployment_target`.
Download `http://gavinandresen-bitcoin.s3.amazonaws.com/boost_macports_fix.zip`
for a fix. Some ports also seem to obey either `build_arch` or
`macosx_deployment_target`, but not both at the same time. For example, building
on an OS X 10.6 64-bit machine fails. Official release builds of notEvilDime-Qt are
compiled on an OS X 10.6 32-bit machine to workaround that problem.

Once dependencies are compiled, creating `notEvilDime-Qt.app` is easy:

    make -f Makefile.osx RELEASE=1

Running
-------

It's now available at `./notevildimed`, provided that you are still in the `src`
directory. We have to first create the RPC configuration file, though.

Run `./notevildimed` to get the filename where it should be put, or just try these
commands:

    echo -e "rpcuser=notevildimerpc\nrpcpassword=$(xxd -l 16 -p /dev/urandom)" > "/Users/${USER}/Library/Application Support/notEvilDime/notevildime.conf"
    chmod 600 "/Users/${USER}/Library/Application Support/notEvilDime/notevildime.conf"

When next you run it, it will start downloading the blockchain, but it won't
output anything while it's doing this. This process may take several hours.

Other commands:

    ./notevildimed --help  # for a list of command-line options.
    ./notevildimed -daemon # to start the notevildime daemon.
    ./notevildimed help    # When the daemon is running, to get a list of RPC commands


The 2017 Boost library
-------

boost can safely be upgraded to the newest version available in brew.

To install:

    (older versions) chmod a+x ./dependencies/boost_1_50_0/tools/build/v2/engine/build.sh
    cd dependencies/boost_1_50_0
    Configure (and build bjam):

    (older versions) chmod a+x bootstrap.sh
    sudo su
    ./bootstrap.sh --prefix=/opt/local
   
Build, sit back and relax while 14000 targets are build

    ./b2
Install:

    ./b2 install
    exit

The newest boost libraries are recommended. Back in 2012 the compilers were more forgiving than
the standard of 2017.
