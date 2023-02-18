A repository with complete documentation of VSD-HDP program

Program: [SKY130-based ASIC Design Projects](https://www.vlsisystemdesign.com/hdp/)

- Author: T S Rakshith, rakshith.ec20@bmsce.ac.in
- Project quick links:

# VSD-HDP Task Status

## Day 0

- Installation of necessary tools

### Yosys
#### Installation Guide
~~~
https://github.com/YosysHQ/yosys
~~~
#### Installation Flow
~~~
$ sudo apt-get install build-essential clang bison flex \
  libreadline-dev gawk tcl-dev libffi-dev git \
  graphviz xdot pkg-config python3 libboost-system-dev \
  libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ mkdir yosys-master
$ cd yosys-master
$ git clone https://github.com/YosysHQ/yosys.git
$ sudo apt install make(installing make if you havent done it yet)
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make
$ sudo install make
~~~
#### Image
![1](https://user-images.githubusercontent.com/112770970/219853505-340c2884-9afc-4229-b735-cea1062c5190.JPG)

### ngspice
#### Installation Guide
~~~
https://sourceforge.net/projects/ngspice/files/
~~~
#### Installation Flow
~~~
$ tar -zxvf ngspice-37.tar.gz
$ cd ngspice-37
$ mkdir release
$ cd release
$ ../configure  --with-x --with-readline=yes --disable-debug
$ make
$ sudo make install
~~~
#### Image
![4](https://user-images.githubusercontent.com/112770970/219853696-ff45fa64-6df9-4a32-8025-b6693187be09.JPG)

### openSTA
#### Installation Guide
~~~
https://github.com/The-OpenROAD-Project/OpenSTA
~~~
#### Installation Flow
~~~
$ sudo apt install swig
$ git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
$ cd OpenSTA
$ mkdir build
$ cd build
$ cmake ..
$ make
~~~
#### Image
![5](https://user-images.githubusercontent.com/112770970/219853789-d533552b-9626-4d14-a86b-183a336b0a60.JPG)

### iverilog
~~~
$ sudo apt-get install iverilog
~~~

### gtkwave
~~~
$ sudo apt update
$ sudo apt install gtkwave
~~~

## Day 1

