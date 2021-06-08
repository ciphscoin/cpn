Launching Ciphscoin Protocol Network [CPN] Software
As tested on Ubuntu 18.04 - No known issue
As tested on Ubuntu 20.04 - No libqt4-dev dependencies for Ubuntu 20.04, use PPA to add one. Then continue as usual.

# Installing dependencies

sudo apt-get update

sudo apt-get install build-essential pkg-config libc6-dev m4 g++-multilib autoconf libtool ncurses-dev unzip git python zlib1g-dev wget bsdmainutils automake libboost-all-dev libssl-dev libprotobuf-dev protobuf-compiler libgtest-dev libqt4-dev libqrencode-dev libdb++-dev ntp ntpdate vim software-properties-common curl libcurl4-gnutls-dev cmake clang


# Install nanomsg

cd ~

git clone https://github.com/nanomsg/nanomsg

cd nanomsg

cmake . -DNN_TESTS=OFF -DNN_ENABLE_DOC=OFF

make -j2

sudo make install

sudo ldconfig

# Compiling Ciphscoin Protocol Netowrk [CPN]

cd ~

git clone https://github.com/ciphscoin/cpn

cd cpn

git checkout dev

./zcutil/fetch-params.sh

rm -r /home/user/.zcash-fetch-params  //needed due to Zcash has moved file locations. Expect to receive 1 error regarding failed checksum.

./zcutil/fetch-params-alt.sh

./zcutil/build.sh -j2

# Launching CPN

cd ~

cd cpn/src

use Screen to attach CPN terminal, execute:
screen -S cpn

Deploy CPN with exact parameter below:
./komodod -ac_name=CIPHS -ac_supply=6000000 -ac_reward=0,9998452,77000000,129680190,210000000,150000000,100000000 -ac_eras=7 -ac_end=7200,50400,2556000,12780000,12780000,17892000,0 -ac_decay=100000000,100000000,100000000,100000000,100000000,100000000,100000000 -ac_halving=1 -ac_adaptivepow=1 -ac_blocktime=12 -ac_cbmaturity=1000 -ac_sapling=1 -ac_snapshot=7200 -ac_cc=313 -ac_ccenable=225,226,227,228,231,232,234,235,236,237,238,239,240,241,242,243 -addnode=152.89.247.97 -addnode=212.114.52.2 &

CTRL A + CTRL D to detach CPN Screen [screen -r cpn to reattach] 
Now launch Ciphscoin mining using cli:

./komodo-cli -ac_name=CIPHS setgenerate true J 
J represent CPU Core. If 4 then set 4. Want to use 2 core, typing 2 it is.

Get wallet address
./komodo-cli -ac_name=CIPHS getaccountaddress ""

For blockhain info
./komodo-cli -ac_name=CIPHS getinfo

To check current circulating supply
./komodo-cli -ac_name=CIPHS getblocksupply >Highest.Block<
Change >highest.block< with current block from getinfo

For all command line available
./komodo-cli -ac_name=CIPHS help

See ya.
