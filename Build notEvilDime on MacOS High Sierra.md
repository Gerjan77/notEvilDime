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
        notEvilDime v1.0.0.0-g88ff655-beta
        Qt version 5.9.3
        OpenSSL OpenSSL 1.0.2m  2 Nov 2017
        
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

Qt 5:
------
Download Qt 5.9.3 from https://download.qt.io/archive/qt/5.9/5.9.3/ and Qt Creator 2.4.0 from https://download.qt.io/archive/qtcreator/2.4/ Open notEvilDime-qt.pro Go to Projects -> Build Settings -> Debug select Qt5.9.3 , Clang (86 64 bit)



notEvilDime-qt.app
-----------------
Compile notEvilDime-qt-mac.pro in Qt Creator 4.4.1 based on Qt 5.9.3, Clang 7.0, 64 bit



    
Deploy
-----------------------
edit the Info.plist not with Xcode, but with a plist editor or iHex

    ~/Documents/GitHub/notEvilDime/Share/qt/Info.plist

Read the deploy tool help

    ~/Qt5.9.3/5.9.3/clang_64/bin/macdeployqt -h

Deploy the bundle

    ~/GitHub/notEvilDime/notEvilDime-Qt.app
    
with the deploy deploy tool.
Deploy MiniUPnPC

    ~/Qt5.9.3/5.9.3/clang_64/bin/macdeployqt ~/GitHub/notEvilDime/notEvilDime-Qt.app -libpath=/opt/local/lib -verbose=3
    
Deploy Openssl

    ~/Qt5.9.3/5.9.3/clang_64/bin/macdeployqt ~/GitHub/notEvilDime/notEvilDime-Qt.app -libpath=/usr/local/opt/openssl/lib -verbose=3
    
Deploy BerkeleyDB

    ~/Qt5.9.3/5.9.3/clang_64/bin/macdeployqt ~/GitHub/notEvilDime/notEvilDime-Qt.app -libpath=/usr/local/opt/berkeley-db@4/lib -verbose=3
    
Deploy the Boost library

    ~/Qt5.9.3/5.9.3/clang_64/bin/macdeployqt ~/GitHub/notEvilDime/notEvilDime-Qt.app -libpath=/usr/local/opt/boost/lib -verbose=3
    
Make sure ˜/Documents/GitHub/notEvilDime/notEvilDime-Qt.app/Contents/Resources/qt.conf contains the following lines:

     [Paths]
       Plugins = PlugIns
    
(optionally) Copy the .app bundle to a FAT32 volume

       /volumes/FAT32/app/notEvilDime-Qt.app


Sign with the apple developer identity in your keychain

    codesign -f -s "3rd Party Mac Developer Application: G.J.A. Uijtdewilligen (CK92ZX6P5T)" -i "com.goodjobunit.notEvilDime" -v /volumes/FAT32/app/notEvilDime-Qt.app
    
Check the signature

    codesign -v --verbose=4 --display /volumes/FAT32/app/notEvilDime-Qt.app
    
Error: unsealed contents present in the bundle root
because four packages are from other developers.

Location of Blockchain and wallet
--------------------------------------
    ls -l -a ~/Library/"Application Support"/notEvilDime



Testing to do
---------------

run the app on a fresh install of MacOS 10.10 Yosemite on the apple account of my beta tester


