Install ROOT from source on your laptop
====

Install the packages:

    sudo apt-get install git dpkg-dev make g++ gcc binutils libx11-dev libxpm-dev \
    libxft-dev libxext-dev

Optional packages:

    sudo apt-get install gfortran libssl-dev libpcre3-dev \
    xlibmesa-glu-dev libglew1.5-dev libftgl-dev \
    libmysqlclient-dev libfftw3-dev cfitsio-dev \
    graphviz-dev libavahi-compat-libdnssd-dev \
    libldap2-dev python-dev libxml2-dev libkrb5-dev \
    libgsl0-dev libqt4-dev

from 

    https://root.cern.ch/build-prerequisites#ubuntu

download ROOT

    git clone http://root.cern.ch/git/root
    mkdir build
    cd build
    cmake -Droofit=ON -Dmathmore=ON ../root -Dtmva=ON
    make -j 20

