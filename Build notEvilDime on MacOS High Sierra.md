# Build notEvilDime on MacOS High Sierra 10.13

Used versions
----------------
    Processor
        3,4 GHz Intel Core i7
    OS
        MacOS High Sierra 10.13
    OS type
        64-bit
    Software
        notEvilDime
        Qt version 5.9.3
        OpenSSL
        
Set the build directory

    GIT=~/Documents/GitHub

Git
---
download Git Desktop https://desktop.github.com
clone the repository https://github.com/Gerjan77/notEvilDime

Brew
------
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Boost library
--------------
brew install boost

edit the BOOST_INCLUDE_PATH and BOOST_LIB_PATH in notEvilDime-qt.pro

    BOOST_LIB_PATH = /usr/local/opt/boost/lib
    BOOST_INCLUDE_PATH = /usr/local/opt/boost/include

edit the location of Boost libraries in src/makefile.osx

    line 12 BOOSTDIR=/usr/local/opt/boost
    

Openssl
---------
brew install openssl
edit the OPENSSL_INCLUDE_PATH and OPENSSL_LIB_PATH in notEvilDime-qt.pro

    OPENSSL_LIB_PATH = /usr/local/opt/openssl/lib
    OPENSSL_INCLUDE_PATH = /usr/local/opt/openssl/include
edit the location of openssl in src/makefile.osx

    line 11 SSLDIR=/usr/local/opt/openssl

BerkeleyDb
-------------
brew search berkeley-db
brew install berkeley-db@4
edit the library and include paths in notEvilDime-qt.pro

    BDB_LIB_PATH = /usr/local/opt/berkeley-db@4/lib
    BDB_INCLUDE_PATH = /usr/local/opt/berkeley-db@4/include
edit the location of BerkeleyDb in src/makefile.osx

    line 13 BERKELEYDIR=/usr/local/opt/berkeley-db@4

Check the versions:

    brew ls --versions

Libminiupnpc:
-------------
    cd ~/Documents/GitHub/notEvilDime/dependencies/miniupnpc-1.6
    sudo su
    INSTALLPREFIX=/opt/local make install
    exit
    
edit the library and include paths in notEvilDime-qt.pro

    MINIUPNPC_INCLUDE_PATH = /opt/local/include
    MINIUPNPC_LIB_PATH = /opt/local/lib

Qt 4:
------
Download Qt 5.9.3 from https://download.qt.io/archive/qt/5.9/5.9.3/ and Qt Creator 2.4.0 from https://download.qt.io/archive/qtcreator/2.4/ Open notEvilDime-qt.pro Go to Projects -> Build Settings -> Debug select Qt5.9.3 , Clang (86 64 bit)



notEvilDime-qt
-----------------
Compile notEvilDime-qt.pro



Location of Blockchain and wallet
--------------------------------------
    ls ~/.notevildime -l
    
    
Find the deploy tool
-----------------------

    ~/Qt5.9.3/5.9.3/clang_64/bin/macdeployqt -h
pass the bundle

    ~/Documents/GitHub/notEvilDime/notEvilDime-qt.app
    ~/Qt5.9.3/5.9.3/clang_64/bin/macdeployqt ~/Documents/GitHub/notEvilDime/notEvilDime-qt.app


Debug

sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils

libzmq3-dev


GIT=~/git
git clone https://github.com/zeromq/libzmq $GIT/libzmq
cd $GIT/libzmq
./autogen.sh
./configure
make -j 4

notEvilDime Deamon

cd notEvilDime/src
make -f makefile.osx
