# GnuRadio3.8-Ubuntu-18
A simple ReadMe to follow for everyone that needs to install GnuRadio 3.8 under Ubuntu 18.
I had many problems to install gnuradio to work with a Nuand SDR with zigbee so I dedided to create a tutorial

# Install GnuRadio 3.8
```
sudo add-apt-repository ppa:gnuradio/gnuradio-releases-3.8
sudo apt install gnuradio
```

## Install 802.15.4 Dependencies
```
sudo apt install swig
sudo apt-get install python-matplotlib
```
## Install Foo
```
git clone https://github.com/bastibl/gr-foo.git
cd gr-foo/
mkdir build
cd build/
cmake ..
sudo make install
sudo ldconfig
```

## Install 802.15.4
```
git clone https://github.com/bastibl/gr-ieee802-15-4.git
cd gr-ieee802-15-4/
mkdir build
cd build/
cmake ..
make
sudo make install
sudo ldconfig
```

Add to .bashrc

```
export PYTHONPATH=/usr/local/lib/python3
export LD_LIBRARY_PATH=/usr/local/lib
source .bashrc 
```

## Run
```
gnuradio-companion
```

# For Nuand SDR

## Install IqBal
```
git clone https://github.com/osmocom/gr-iqbal.git
cd gr-iqbal/
git checkout gr3.8
git submodule update --init --recursive
mkdir build
cd build/
cmake ..
make
sudo make install
sudo ldconfig
```
## Install BladeRF
```
git clone https://github.com/Nuand/bladeRF.git
cd bladeRF/
git checkout 2021.02 
cd host/
mkdir -p build
cd build/
git submodule update --recursive
cmake ..
make
sudo make install
sudo ldconfig
```
## Install Osmo SDR
`git clone git://git.osmocom.org/gr-osmosdr`

In CMakeFile.txt
replace: 
```
find_package(gnuradio-iqbalance PATHS ${Gnuradio_DIR})`
```
with: 
```
find_package(gnuradio-iqbalance PATHS /usr/local/lib/cmake/gnuradio/)
```
Then:
```
cd gr-osmosdr/
mkdir build
cd build/
cmake ..
make
sudo make install
sudo ldconfig
```

# Add plugdev to User
```
sudo apt install libusb-1.0-0-dev 
sudo usermod -a -G plugdev $User
```
Logout to aply the new rules
