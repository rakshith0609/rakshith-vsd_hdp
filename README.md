**A repository with complete documentation of VSD-HDP program**

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

**Create directory for labs:**
~~~
mkdir vsd
cd vsd
mkdir VLSI
cd VLSI
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop
~~~

### Logic Cell Simulation
- Simulated xor gate using good mux

### Code:
![3](https://user-images.githubusercontent.com/112770970/219854973-77b592c2-1242-4833-be4d-0f0e876e7652.JPG)

![2](https://user-images.githubusercontent.com/112770970/219854982-2e088b13-42df-4942-9b20-05b726fa4e51.JPG)

### Commands:
~~~
$ cd verilog_files
$ iverilog xor_gate_using_good_mux.v xor_gate_using_good_mux_tb.v
$ ./a.out 
$ gtkwave xor_gate_using_good_mux_tb.vcd
~~~

### Waveforms generated:
![lab1](https://user-images.githubusercontent.com/112770970/219855091-c3a346c6-cb38-4334-bd2d-c59fd6b9a560.JPG)

### Logic Cell Synthesis
- Synthesized xor gate using good mux

### Commands:
~~~
$ yosys
> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> read_verilog xor_gate_using_good_mux.v good_mux.v
> synth -top xor_gate_using_good_mux
> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> show xor_gate_using_good_mux
~~~

### Synthesis Schematic:
![4](https://user-images.githubusercontent.com/112770970/219855345-f7673c7c-b315-458c-968d-450a13000139.JPG)
![6](https://user-images.githubusercontent.com/112770970/219855446-75760430-3d76-4d81-a6aa-d023478dad3b.JPG)

![5](https://user-images.githubusercontent.com/112770970/219855385-f4d4dc9d-5034-4628-9097-b007bf09c1af.JPG)

### Commands to generate netlist:
~~~
> write_verilog -noattr good_mux_netlist.v
>!gvim good_mux_netlist.v
~~~

![8](https://user-images.githubusercontent.com/112770970/219855472-1ce2e662-69f7-4a3d-a976-f768c50463c7.JPG)



## Day 2

### Important notes
- Standard Cell Library files will contain details of all types of individual cells with different parameters of area, power and delay.
- PVT corners different for different .lib files
- Hierarchical v/s Flat Synthesis.
- To aviod glitch propagation in multiple combinational blocks, flip flops are used to stabilize data before each combinational block.
- Asynchronous and synchronous reset/set with D_FF explored.

### Commands
~~~
$ yosys
> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> read_verilog multiple_modules.v
> synth -top multiple_modules
> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> show multiple_modules
> write_verilog -noattr multiple_modules_hier.v
> flatten
> write_verilog -noattr multiple_modules_flat.v
~~~

### Synthesis Schematic and netlist for multiple modules:
![3](https://user-images.githubusercontent.com/112770970/219856449-00bdabd6-3f8f-4382-858a-7b7b5cb828cb.JPG)

![1](https://user-images.githubusercontent.com/112770970/219856497-04ea6607-1bfd-4571-8a71-248c019176ad.JPG)

![4](https://user-images.githubusercontent.com/112770970/219856455-dc79ae75-d879-4c20-8e4a-ba3fec07ea69.JPG)

### Flat Synthesis
![5](https://user-images.githubusercontent.com/112770970/219856481-5616038e-c92f-4155-89f6-c5da338a5e95.JPG)

### D-Flip Flop Synthesis

Use addtional command:
~~~
$ > dfflibmap -liberty <.lib file path>
~~~

Asynchronous reset:
![asynch_reset syn](https://user-images.githubusercontent.com/112770970/219856560-2ec3e92e-3407-4c05-bf1a-228b95236cfa.JPG)

Synchronous reset:
![synch_reset synthesis](https://user-images.githubusercontent.com/112770970/219856579-7368ea1f-cb77-47e5-8e94-3f54eeb614de.JPG)

### D-Flip FLop Simulation
Asynchronous reset:

![asynch_reset wave](https://user-images.githubusercontent.com/112770970/219856663-2603d11c-efe8-4f17-ac1a-627dc94a15e0.JPG)

Synchronous reset:

![synch_reset](https://user-images.githubusercontent.com/112770970/219856669-6514e587-a19c-40c8-84df-4bd1635636a4.JPG)

### Interesting Optimizations:

#### Synthesis of some special functions:

- mult_2.v : y = 2 * a; where y is 4 bit and a is 3 bit number

![opt1](https://user-images.githubusercontent.com/112770970/219856933-8d6e4b57-3f85-4f09-b9cf-c1c55640e13d.JPG)
![6](https://user-images.githubusercontent.com/112770970/219856940-bd3dff20-d47d-4409-a761-02d4034cfd5b.JPG)

- mult_8.v : y = 9 * a; where y is 6 bit and a is 3 bit number 

![opt2](https://user-images.githubusercontent.com/112770970/219857110-11a15a81-a286-4986-af93-a03f5cae29da.JPG)
![7](https://user-images.githubusercontent.com/112770970/219857004-f9c586ba-d3b2-4f4b-acea-63524538e85e.JPG)

- **In these cases, no circuit is synthesised**


## Day 3

### Logic Optimisations
- Combinational Logic Optimisation
  * Constant Propagation
  * Boolean Logic Optimasation
  
- Sequential Logic Optimisation
  * Sequential Constant Propagation
  * State Optimisation
  * Retiming
  * Sequential logic cloning

### Important Points
- Optimisation is done to reduce unused states and redundancy.
- In state optimisation, unused states are removed.
- In sequential logic cloning, addtional flops are added to increase positive slack when the other flops in the design are placed far apart in the floorplan to meet their timing requirements.
- In retiming, the combinational blocks between different flops are modelled such that their clock frequency increases without violating setup and hold, thereby, increasing performance.

### Additional Command to use:
~~~
$ > opt_clean -purge
~~~

### Synthesis Illustating Sequential Constant Propagation:
- In this case, the flip flop is redundant.

![dff_const4_syn](https://user-images.githubusercontent.com/112770970/219862146-472e3e1a-8f37-4141-ad9c-41887ef9b774.JPG)

![dff_const5_syn](https://user-images.githubusercontent.com/112770970/219862301-bb179eda-0dd5-4ddf-ab25-c005795ecf7a.JPG)

### Simulation Illustating Sequential Constant Propagation:
- In this case, the output q always remains 1, therefore flip flop is not needed.
  
![dff_const4_wave](https://user-images.githubusercontent.com/112770970/219862898-284bc9b5-bc93-489f-a125-9eea03a87526.JPG)

![dff_const5_wave](https://user-images.githubusercontent.com/112770970/219862976-c340e657-6fef-402b-b7d9-00516d301660.JPG)

### Combinational Logic Optimisations

### Logic used in opt_check4.v :
~~~
 assign y = a ? (b ? (a & c) : c) : (!c);
~~~

![opt_check_4](https://user-images.githubusercontent.com/112770970/219863972-5bd9f48a-c1ab-4741-a335-8d17e4fa553e.JPG)
![opt_check_4_cells](https://user-images.githubusercontent.com/112770970/219863977-574f6e43-0a48-4efe-824a-cfb8daff07e4.JPG)

### Synthesis of multiple_modules file:

![multiple_modules_opt](https://user-images.githubusercontent.com/112770970/219864034-3b9e57d2-6528-4dca-9755-fe2f206682ac.JPG)

### Synthesis of unused output (3-bit Counter example) :

![counter_opt1](https://user-images.githubusercontent.com/112770970/219864111-d46d1829-467a-468f-9b26-f77ab72cf9a9.JPG)

### Synthesis if all output ports are used (3-bit Counter example) :

![counter_opt2](https://user-images.githubusercontent.com/112770970/219864154-864adb26-e33a-4abb-9647-8415fd40ecb7.JPG)



## Day 4
