# Build notEvilDime on MacOS High Sierra 10.13

Used versions
-------------

    Processor
        3,4 GHz Intel Core i7
    OS
        MacOS High Sierra 10.13
    OS type
        64-bit
    Software
        notEvilDime
        Qt version 4.8.1
        OpenSSL

Set the build directory
-----------------------

    GIT=~/Documents/GitHub


Git
----

    download Git Desktop https://desktop.github.com
    clone the repository https://github.com/Gerjan77/notEvilDime
	
Brew
-----

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

	
Boost library
--------------

    brew install boost

Openssl
---------

    brew install openssl
edit the OPENSSL_INCLUDE_PATH and OPENSSL_LIB_PATH in notEvilDime-qt.pro

    OPENSSL_LIB_PATH = /usr/local/opt/openssl/lib
    OPENSSL_INCLUDE_PATH = /usr/local/opt/openssl/include



BerkeleyDb
--------------
    brew search berkeley-db
    brew install berkeley-db@4
edit the library path -L in notEvilDime-qt.pro
edit the library and include paths in notEvilDime-qt.pro

    BDB_LIB_PATH = /usr/local/opt/berkeley-db@4/lib
    BDB_INCLUDE_PATH = /usr/local/opt/berkeley-db@4/include

Check the versions:

    brew ls --versions

Libminiupc:
-----------

    cd ~/Documents/GitHub/notEvilDime/dependencies/miniupnpc-1.6
    sudo su
    INSTALLPREFIX=/opt/local make install
    exit




Qt 4:
-----
Download Qt 4.8.1 from https://download.qt.io/archive/qt/4.8/4.8.1/
and Qt Creator 2.4.0 from https://download.qt.io/archive/qtcreator/2.4/
Open notEvilDime-qt.pro
Go to Projects Build Settings Debug
select Qt4.8.1 , Clang (86 64 bit)


boost
-----

	sudo apt-get install libboost1.48

notEvilDime
-----------


	https://github.com/Gerjan77/notEvilDime

BerkeleyDB
----------

	BDB="${NED}/db4"
	mkdir -p $BDB
	wget 'http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz'
	echo '12edc0df75bf9abd7f82f821795bcee50f42cb2e5f76a6a281b85732798364ef  db-4.8.30.NC.tar.gz' | sha256sum -c
	tar -xzvf db-4.8.30.NC.tar.gz
	cd db-4.8.30.NC/build_unix/
	../dist/configure --enable-cxx --disable-shared --with-pic --prefix=$BDB
	make install

Configure notEvilDime Core to use our own-built instance of BDB
---------------------------------------------------------------

	cd $NED
	make
	make install (optional)

Location of Blockchain and wallet
---------------------------------

	ls ~/.notevildime -l

	



Debug
---------------------
    sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils
    libzmq3-dev
    -----------
    
    GIT=~/git
    git clone https://github.com/zeromq/libzmq $GIT/libzmq
    cd $GIT/libzmq
    ./autogen.sh
    ./configure
    make -j 4
    
