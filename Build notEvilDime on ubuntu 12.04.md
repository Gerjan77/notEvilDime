GIT=~/git
mkdir $GIT

# Update gcc (Solution of: Configure: error: *** A compiler with support for C++11 language features is required)

sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install gcc-4.9 g++-4.9
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 60 --slave /usr/bin/g++ g++ /usr/bin/g++-4.9
sudo apt-get install gcc-4.8 g++-4.8
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 60 --slave /usr/bin/g++ g++ /usr/bin/g++-4.8
sudo update-alternatives --config gcc

# Git:
sudo apt-get install git

# Boost library:
sudo apt-get install libboost1.48-all-dev

# Build requirements:
sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils

# Libminiupc:
sudo apt-get install libminiupnpc-dev

# libzmq3-dev
GIT=~/git
git clone https://github.com/zeromq/libzmq $GIT/libzmq
cd $GIT/libzmq
./autogen.sh 
./configure 
make -j 4

# Qt 4:

sudo apt-get install libqt4-dev libprotobuf-dev protobuf-compiler

# boost
sudo apt-get install libboost1.48

# notEvilDime:

NED=$GIT/NotEvilDime
git clone https://github.com/Gerjan77/notEvilDime $NED

# BerkeleyDB

BDB="${NED}/db4"
mkdir -p $BDB
wget 'http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz'
echo '12edc0df75bf9abd7f82f821795bcee50f42cb2e5f76a6a281b85732798364ef  db-4.8.30.NC.tar.gz' | sha256sum -c
tar -xzvf db-4.8.30.NC.tar.gz
cd db-4.8.30.NC/build_unix/
../dist/configure --enable-cxx --disable-shared --with-pic --prefix=$BDB
make install

# Configure notEvilDime Core to use our own-built instance of BDB
cd $NED
(fail)./autogen.sh
(fail)./configure LDFLAGS="-L${BDB}/lib/" CPPFLAGS="-I${BDB}/include/" USE_UPNP=-
make
make install (optional)







FAIL: 

libzmq3 :no after configure litecoin. 


$ sudo chmod a+rw+ /etc/apt/sources.list
$ echo "deb http://download.opensuse.org/repositories/network:/messaging:/zeromq:/release-stable/Debian_9.0/ ./" >> /etc/apt/sources.list
$ wget https://download.opensuse.org/repositories/network:/messaging:/zeromq:/release-stable/Debian_9.0/Release.key
$ sudo apt-key add Release.key
apt-get install libzmq3-dev

BerkelyDB:
tar -xzvf db-4.8.30.NC.tar.gz
cd db-4.8.30.NC/build_unix/
../dist/configure --enable-cxx
make
sudo make install

Tell your system where to find db4.8
export BDB_INCLUDE_PATH="/usr/local/BerkeleyDB.4.8/include"
export BDB_LIB_PATH="/usr/local/BerkeleyDB.4.8/lib"
sudo ln -s /usr/local/BerkeleyDB.4.8/lib/libdb-4.8.so /usr/lib/libdb-4.8.so

TODO

git clone https://github.com/zeromq/libzmq
./autogen.sh && ./configure && make -j 4
make check && make install && sudo ldconfig

Or, using CMake:

git clone https://github.com/zeromq/libzmq
mkdir cmake-build && cd cmake-build
cmake .. && make -j 4
make test && make install && sudo ldconfig

To build from master on Windows using VS2015:

git clone https://github.com/zeromq/libzmq
cd libzmq\builds\msvc
configure
cd build
buildall


