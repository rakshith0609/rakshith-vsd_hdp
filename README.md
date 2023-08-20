**A repository with complete documentation of VSD-HDP program**

Program: [SKY130-based ASIC Design Projects](https://www.vlsisystemdesign.com/hdp/)

- Author: T S Rakshith, rakshith.ec20@bmsce.ac.in

Progress Quick-Link:<br />
- [DAY_0](https://github.com/rakshith0609/rakshith-vsd_hdp/main/README.md#Day_0)
- [DAY_1](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-1)
- [DAY_2](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-2)
- [DAY_3](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-3)
- [DAY_4](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-4)
- [DAY_5](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-5)
- [DAY_6](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-6)
- [DAY_7](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-7)
- [DAY_8](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-8)
- [DAY_9](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-9)
- [DAY_10](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-10)
- [DAY_11](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-11)
- [DAY_12](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-12)
- [DAY_13](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-13)
- [DAY_14](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-14)
- [DAY_15](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-15)
- [DAY_16](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-16)
- [DAY_17](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-17)
- [DAY_18](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-18)
- [DAY_19](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-19)
- [Day_20](https://github.com/rakshith0609/rakshith-vsd_hdp/main/README.md#Day_20)
- [DAY_21](https://github.com/Visruat/Visruat-VSD-HDP/blob/main/README.md#day-21)

# VSD-HDP Task Status

## Day_0

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


------


## Day_1

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
- Synthesised xor gate using good mux

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


------


## Day_2

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

- **In these cases, the cells in the standard cell library won't be mapped as only nets are realised.**


------


## Day_3

### Logic Optimizations
- Combinational Logic Optimization
  * Constant Propagation
  * Boolean Logic Optimasation
  
- Sequential Logic Optimization
  * Sequential Constant Propagation
  * State Optimization
  * Retiming
  * Sequential logic cloning

### Important Points
- Optimization is done to reduce unused states and redundancy.
- In state optimization, unused states are removed.
- In sequential logic cloning, addtional flops are added to increase positive slack when the other flops in the design are placed far apart in the floorplan to meet their timing requirements.
- In retiming, the combinational blocks between different flops are modelled such that their clock frequency increases without violating setup and hold, thereby, increasing performance.

### Additional Command to use:
~~~
$ > opt_clean -purge
~~~

### Synthesis Illustrating Sequential Constant Propagation:
- In this case, the flip flop is redundant.

![dff_const4_syn](https://user-images.githubusercontent.com/112770970/219862146-472e3e1a-8f37-4141-ad9c-41887ef9b774.JPG)

![dff_const5_syn](https://user-images.githubusercontent.com/112770970/219862301-bb179eda-0dd5-4ddf-ab25-c005795ecf7a.JPG)

### Simulation Illustrating Sequential Constant Propagation:
- In this case, the output q always remains 1, therefore flip flop is not needed.
  
![dff_const4_wave](https://user-images.githubusercontent.com/112770970/219862898-284bc9b5-bc93-489f-a125-9eea03a87526.JPG)

![dff_const5_wave](https://user-images.githubusercontent.com/112770970/219862976-c340e657-6fef-402b-b7d9-00516d301660.JPG)

### Combinational Logic Optimizations

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


------


## Day_4

### Gate Level Synthesis
- logical verification
- ensuring timing is met
- gate level verilog model is fed to the iverilog block along with the design and testbench

### Simulation-Synthesis Mismatch
- missing sensitivity list
- correct usage of blocking and non blocking assignments
- bad coding style
- Non blocking assignments must be used for sequential circuits

### Bad Mux Example
- Simulation of bad_mux

![bad_mux sim](https://user-images.githubusercontent.com/112770970/221162808-0cbf452d-4b55-4915-a101-bf1cecc028c5.JPG)


- Synthesis of bad_mux

![bad_mux synth](https://user-images.githubusercontent.com/112770970/221163038-f39f861b-60d5-4ed8-a888-2006b6cdee5c.JPG)


- Simulation of the gate level netlist generated

![bad_mux _netlist_sim](https://user-images.githubusercontent.com/112770970/221163175-f4eb136e-20b1-4f3d-92ce-f75b7156ecb5.JPG)

- It can be seen above that there clearly exists a simulation synthesis mismatch.
- Synthesis gave the correct waveform and no latch was inferred.
- Simulation indicates the behaviour of a latch.

### Blocking Assignment Caveat
- Simulation

![BA sim](https://user-images.githubusercontent.com/112770970/221163838-b6063b1c-b192-4fdd-9928-1a76642e510f.JPG)


- Synthesis

![BA synth](https://user-images.githubusercontent.com/112770970/221163927-37720a22-213c-46a2-a705-5cad774c4cf9.JPG)


- Simulation of the gate level netlist generated

![BA netlist sim](https://user-images.githubusercontent.com/112770970/221163993-3e7f7f23-e216-4db9-813c-f27e9a275072.JPG)

- A delay/flop behaviour can be observed in the simulation waveform.
- This design also results in a simulation synthesis mismatch.


------


## Day_5

### If and Case Statements
- Both if and case statements infer muxes but if statements have priority logic.
- Incomplete if and case statements infer an unwanted latch.
- All the outputs must be specified inside all the sub-cases else latches are inferred.
- Overlapping cases in the case statements leads to ambiguous output.

### Incomplete If statements
- Simulation

![incomp if sim](https://user-images.githubusercontent.com/112770970/221235513-28a617ec-2217-452d-aa18-8230dea43691.JPG)


- Synthesis

![incomp if synth](https://user-images.githubusercontent.com/112770970/221235733-9426a6fe-b288-4430-9b38-e4e33bf6943b.JPG)

- It can be seen that a latch is inferred as shown above.

### Incomplete Case statements
- Simulation

![incomp case sim](https://user-images.githubusercontent.com/112770970/221245695-f79c6153-4a55-47a4-9aba-230700f5080b.JPG)


- Synthesis

![incomp case synth](https://user-images.githubusercontent.com/112770970/221245793-50a20891-670b-4868-b1ba-96087b354c85.JPG)

- It can be seen that a latch is inferred as shown above.

- The solution for the above problem is specifiying the default case.

- The simulation and synthesis of case with default is shown below:

![case with default sim](https://user-images.githubusercontent.com/112770970/221246682-7f36c4e3-bd66-4f9d-ab7c-2abba9e2f100.JPG)

![case with default synth](https://user-images.githubusercontent.com/112770970/221246740-f4472080-c4a9-499c-a439-2c2d57002295.JPG)


### Output register not assigned in a particular subcase
- Simulation

![bad case sim](https://user-images.githubusercontent.com/112770970/221247206-472daa5f-7639-4549-b40e-5964dc563941.JPG)


- Simulation of the generated netlist (GLS)

![bad case netlist sim](https://user-images.githubusercontent.com/112770970/221247470-a7563c7c-7c9a-4c9f-9ff2-a4a709a9f606.JPG)


- It can be seen that there exists a simulation synthesis mismatch in this case as output in a particular subcase is not specified.


### Loop and Generate Constructs
- Loops are used to reduce the size of the RTL code in any complex situation.
- Generate blocks are used to instantiate modules many times, in other words, it replicates hardware.

### 1 x 8 Demux using for statements
- Simulation

![demux for loop sim](https://user-images.githubusercontent.com/112770970/221248795-322a358b-99f7-483f-9dc9-485b2cfab4f1.JPG)


- Synthesis

![demux for loop synthJPG](https://user-images.githubusercontent.com/112770970/221248861-b544f89e-a1d7-486b-af74-c6aa24d935a3.JPG)


- Simulation of gate level netlist

![demux for loop netlist sim](https://user-images.githubusercontent.com/112770970/221249009-791bbc62-7271-4ad1-8efb-2321d9fcee95.JPG)

- It can be observed that there is no simulation synthesis mismatch arising in this case.

### Ripple carry adder using generate loop
- Simulation

![rca sim](https://user-images.githubusercontent.com/112770970/221249549-a1500b22-11fa-434a-bda6-f42a118a4bf8.JPG)


- Synthesis

![rca synth](https://user-images.githubusercontent.com/112770970/221249636-2c05ba2b-bde2-43bd-8865-56d57f9ec640.JPG)


- Simulation of gate level netlist

![rca netlist sim](https://user-images.githubusercontent.com/112770970/221249716-cd59ad25-789d-4929-a82e-c8c3633d360d.JPG)

- It can be observed that there is no simulation synthesis mismatch arising in this case.


------



## Day_6

- Design chosen: **8-bit ALU**

- Simulation

![alu sim](https://user-images.githubusercontent.com/112770970/224483732-2948a179-e8ea-4b67-9b1e-b7284c22a2dc.JPG)


- Synthesis

![alu synth](https://user-images.githubusercontent.com/112770970/224483750-733e9c26-dbdf-4df1-a12b-05392c149721.JPG)


- Simulation of gate level netlist (GLS)

![netlist sim alu](https://user-images.githubusercontent.com/112770970/224483778-c4b6d93c-84fc-43c3-847e-0f5739c3d3ce.JPG)

- Design is simulated and synthesized. No simulation-synthesis mismatch is reported.


------


## Day_7

- **Basics of STA**
  * Delay of a cell is a function of input transition and output load.
  * Timing arcs -> combinational and sequential
  * Setup and hold time for a latch and flip flop is around the sampling point.
  * In positive level triggered latch, setup time is before the falling edge (last sampled point).
  * In negative level triggered latch, setup time is before the rising edge (last sampled point).


- **Timing paths**
  * Clock to D pin (register to register)
  * Clock to output (register to out)
  * Input to D pin  (input to register)
  * Input to output 
  

- **Max and Min delay constraints**
  * Calculating maximum frequency of clock and modelling combinational delay
  * Input external delay and output external delay
  * Constraints need to included in the library file which models the input and output external delay. To include practical cases, we need to model this delay while specifying the input transition and output load.
  * Modeling of load capacitance (max value must be specified)
  * Using buffers to reduce fanout, thereby, decreasing the max load capacitance.


- **Lookup table**
  * 2D table consisting of corresponding output load and input transistion values
  * Values in between not specified are calculated through interpolation.
  

- *Unateness
  * Positive unateness -> AND OR
  * Negative unateness -> NAND NOR NOT
  * Non-unateness -> XOR XNOR

- Note: All the above considerations are specified in the .lib file.


------


## Day_8

**Advanced Constraints**
  * Reg to reg path constrained by clock
  * I/P to Reg path -> clock, input delay, input transition 
  * Reg to Out path -> clock, output delay, output load
  * Clocks not arriving at the same time for different registers -> CTS
  * Clock skew to be eliminated post CTS
  * Clock Jitter -> arises due to stochastic variation of clock generation
  * Clock Uncertainty -> clock jitter + clock skew -> to be minimized post CTS
  * Clock Modelling -> period, source latency, clock network latency, clock skew

**Lab8_circuit timing report**

![lab8_circuit](https://user-images.githubusercontent.com/112770970/230723695-38337455-fc9e-486b-abb7-6753a7a1ddca.JPG)


------


## Day_9

**ALU Code Snippet**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/36455704-a8e9-4599-baf0-88fc0c02d066)
![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/8c66e91d-52e4-41bb-afca-0c68c1d17acd)


**ALU Netlist snip**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/5065e342-1bce-4edd-b9b8-f8d6b66379d5)

- It can be seen from the synthesized netlist that there is **no reg to reg path**. There are a total of **8 flops** inferred which is connected to input and output pins parallelly.

**ALU Constraint file:**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/7261fc8f-797d-4c50-94ba-0553dfacc1e8)


**Timing reports**

![alu_timing1](https://user-images.githubusercontent.com/112770970/230723784-ec4ef32d-40bc-4b6c-878b-a3f4862909df.JPG)

![alu_timing2](https://user-images.githubusercontent.com/112770970/230723790-0dc7a432-f651-448b-8530-3fc7d751aa08.JPG)

![alu_timing3](https://user-images.githubusercontent.com/112770970/232210384-7b617190-19df-4b12-89ad-b234ed5eb27f.JPG)


------


## Day_10

- SPICE simulations are needed for generating delay tables needed for STA.

- The delays mainly depend on W/L values which is modelled

**Introduction to MOS Transistors**

- 4 terminal device
- The channel formed is controlled by lateral and vertical electric fields due to Vds and Vgs respectively.
- Three regions od operation:
   * Linear/Resistive -> when Vds is very small
   * Triode -- when Vds < Vgs - Vt and Vgs > Vt
   * Saturation -- when Vds >= Vgs - Vt
- Body effect increases the threshold voltage.
- Channel pinch-off occurs in saturation region and channel length modulation effect should be included in the Id equation.
- Two types of current in the channel
   * drift current (due to potential difference)
   * diffusion current (due to difference in carrier concentration)

**Spice Simulation**

- SPICE model parameters and SPICE netlist given to the SPICE software will generate waveform for analysis

**Spice Simulation of NMOS Ids vs Vds**

![image](https://user-images.githubusercontent.com/112770970/235860955-1d894b49-10ca-471b-813e-51eb48e56e2b.png)

- The above plot is for CMOS inverter and different values on the plot are shown.


------


## Day_11

**SPICE Netlist with same W/L ratio**

![image](https://user-images.githubusercontent.com/112770970/235877401-f33f734d-3623-4e94-87b7-f55f0b468546.png)


**Spice Simulation of NMOS Id vs Vds for W = 0.39u and L = 0.15u**

![image](https://user-images.githubusercontent.com/112770970/235878444-113002a7-a61a-4902-a7dd-5f86ffa82b4a.png)

- It can be seen that compared to the previous Id vs Vds graph that the saturation current slightly increases even though W/L ratio remains constant
- This is because of short channel effect

**Spice Simulation of NMOS Id vs Vgs for W = 0.39u and L = 0.15u**

![image](https://user-images.githubusercontent.com/112770970/235885447-f66488df-2eee-441b-8cab-1c66dd9c1166.png)

**Spice Simulation of NMOS Id vs Vgs for W = 3.12u and L = 1.20u**

![image](https://user-images.githubusercontent.com/112770970/235886466-a4f18b1d-71aa-41ec-841b-d50a71600d88.png)

- It can be seen from the even though the W/L ratio remains 2.6 for both the plots, Id is slightly different. Short channel transistor characteristics has more linearity than the long channel one.


**Velocity Saturation**

- At higher electric fields, the electrons velocity becomes constant.
- This happens in short channel as the electric field strengh increases due to reduced channel length.

**VTC**

- Used to calculate the delay tables for STA.
- The plot of Vout vs Vin in CMOS inverter.


------



## Day_12

**Spice Netlist for inverter**

![image](https://user-images.githubusercontent.com/112770970/235947980-3f11d4d5-c516-4dab-9b09-72157becbea0.png)


**Spice Simulation of Voltage transfer characteristics of CMOS inverter**

![image](https://user-images.githubusercontent.com/112770970/235947067-113ce1da-5fab-4325-9e6f-4a6b1a797a05.png)

- It can be seen that the switching threshold is around 8.76 V.


------


## Day_13

**Spice Simulation of Inverter Switching transition**

![image](https://user-images.githubusercontent.com/112770970/236589265-21aa2016-050d-4017-a8e3-0d36edc9ad50.png)

- From the above simulation delay values for rise and fall can be observed.
- Rise Time --> 0.375 ns
- Fall Time --> 0.2321 ns
- The delay values of different inverters with increased pmos W/L ratio can be found.
- It is seen that the value of rise delay decreases and fall delay increases with increase in W/L of pmos.


------


## Day_14

**Noise Margin**
~~~
    NMH = VOH-VIH // High noise margin
    NML = VIL-VOL // Low noise margin
~~~

**Calculation of Noise Margin from VTC**

![image](https://user-images.githubusercontent.com/112770970/236591730-5514b64f-cc56-4706-bd04-84d9d3c6a4d1.png)

- From the above figure, VIL = 0.790323 V, VOH = 1.67111 V, VIH = 0.964516 V, VOL = 0.128889 V
- NMH = 0.7065 V 
- NML = 0.6614 V


------


## Day_15

**Spice Simulation of Power Supply Scaling**

![image](https://user-images.githubusercontent.com/112770970/236592704-4ef2d4fa-e0bd-4aec-9eb9-a5d65a8c5e2a.png)

- It can be observed by the above values that the gain increases as power supply is reduced upto 1.2 V and after 1 V it starts decreasing.

**Spice Simulation of Device Variation**    
    
![image](https://user-images.githubusercontent.com/112770970/236593273-62f5ad8c-bd7d-4e26-b07c-d51c210fb1c6.png)

- The swithing threshold is observed to be around 0.98 V.
- The pmos W/L ratio is more than its nmos counterpart due to which the pmos charges the load capacitor more.


------


## Day_16

**STA on alu.v with different ss,ff,tt PVT corners**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/ab64e9b1-5650-4327-b22e-97d743d83f38)

- Note --> timing reports of each ss,ff,tt corner is in the files above in this repository.

**Plot of TNS,WNS,WHS with multiple corners**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/3a64bd29-de2d-4b70-87f2-4b30a22addc7)


------


## Day_17

**Inception of Openlane and sky130 pdk**

**Key Notes**

- The chip in general contains many cores which are known as foundary IPs. These can be PLL, SRAM, DAC etc.
- The general flow from applicaton software down to the hardware with system software block in between.
- System Compiler consists of the OS, Compiler and the assembler.
- OS handles I/O operations, memory management, process management and low level system functions.
- Compliler converts high level code into the respective low level code according to hardware (ARM, Intelx86, RISCV, MIPS etc).
- Assembler converts low level machine instructions (ISA) into binary streams.
- Hardware description is written in HDL for respective ISA to follow PD flow.

**What is PDK?**

- PDK (process design kit) is the interface between the FAB and the designers.
- It contains a collection of files used to model a fabrication process for the EDA tools used to design an IC.

**RTL TO GDSII flow**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/89a42e85-dbc7-4b83-87fb-f409d691528c)


- Placement is done in 2 steps after floor planning:
  * Global --> tries to find optimal position for all cells. Such cells are not neccesarily legal. There is overlapping of cells.
  * Detailed --> placements obtained from global are minimally altered to be legal.

- Create a clock distribution network
  * To deliver the clk to all sequential elements in a circuit with minimum skew.

- Route
  * Implement the interconnect using the available metal layers.
  * The skywater pdk contains all the data about the interconnect layer.
  * Metal tracks form a routing grid.

- Physical Verification --> DRC and LVS
- Timing Verification --> STA
- OpenLANE --> produce clean (no DRC, LVS, timing violations) GDSII with no human intervention..

- DFT (Design for Testing)
  * Scan insertion
  * Automatic Test Pattern Generation (ATPG)
  * Test Patterns Compaction
  * Fault Coverage
  * Fault Simulation

- Physical Implementation (Automatic PNR)
  * Floor/Power planning
  * End Decoupling capacitors and tap cell insertion
  * Placement
  * Post Placement Optimization
  * CTS
  * Routing

- Logic Equivalency Check (LEC)
  * The netlist and the output file of the physical implementaion is checked.
  * Everytime the netlist is modified, verification must be performed. (CTS modifies the netlist and so does post placement optimizations).
  * LEC is used to formally confirm that the function did not change after modifying the netlist.

- Dealing with Antenna Rules Violations
  * When a metal wire segment (long enough) is fabricated, it can act as an antenna.
  * Reactive ion etching causes charge to accumulate on the wire.
  * Transistor gates can be damaged due to this during fabrication.
  * Limit the length of the interconnect to address this issue.
  * Add a fake antenna diode next to every cell input after placement.

**OpenLane Labs**

- Invoking openlane and run synthesis for picorv32a design.

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/e63340c2-2492-42a3-8110-dd21d828973a)


------


## Day_18

**Chip Floorplan Considerations**

- Define width and height of core and die
  * A core is the section of the chip where the fundamental logic of the design is placed.
  * A die which consists of the core, is a small semiconductor material specimen on which the fundamental circuit is fabricated.

```
Utilization factor = (area occupied by netlist) / (total area of core)
Aspect ratio = height/width
```
- Define the location of pre-placed cells
  * Bigger combinational blockes (> 100k gates) is divided and implemented separately.
  * The main idea is that they can be implemented once and reused multiple times.
  * These type of cells like memory, clock gating cell, comparator, mux etc. are called pre-placed cells. 
  * They are placed only once before placement and routing of other modules.
  * The arrangement of these IPs in a chip is reffered as floorplanning.
  * These IPs have user defined locations and hence are placed in chip before automated placement and routing and are called as pre-placed cells.
  * Automatic PNR tools places the remaining logical cells in the design onto chip.

- Surround pre-placed cells with decoupling capacitors
  * Due to the distance between the source and the cell, the interconnect has resistance due to which there is a voltage drop.
  * If this voltage drop is more than the noise margin, then the cells are operated in the undefined region.
  * Use of decoupling capacitors will store charges to compensate for the drop which occurs due to interconnect and other losses and ensures operation within noise margin.

- Power Planning
  * Use multiple sources at different locations to aviod ground bounce and droop.

- Pin placement
  * Placement of pins is in accordance with pre-placed cells, where the logical blocks are nearest to the respective pin.
  * Clock pins thickness is more as it drives the signal to the entire chip (less resistance, more area).

- Logical cell placement blockage

**Viewing floorplan of picorv32a in magic**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/b6d19665-3077-48af-917a-296d9a28a8f5)


**Library Binding and Placement**

- Bind netlist with physical cells
  * Library will have cells of different physical dimension and timing constraints.

- Placement of the netlist on the floorplan
- Optimize placement (add repeaters)

**Placement of cells in picorv32a**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/d2654d14-370e-4c15-8479-24d0adbd2dee)

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/9c70baa2-5e83-4e01-96ce-161a32c50fe7)


**Need for Characterization**
- In the physical design flow from logic synthesis --> floorplanning --> placement --> CTS --> Routing, physical cells (gates) are common throughout.
- We need to model and characterize these cells for each stage.

**Cell Design Flow**

- Standard cell library contains all different types of cells with different area, power and timing contraints.
- Inputs --> PDKs, DRC, LVS rules, spice models, library and user defined specs.
- Design Steps --> Circuit design, layout design and characterization
- Outputs --> CDL(circuit description language), GDSII, LEF, extracted spice netlist

**Characterization Flow**

- Read the model files
- Read the extracted spice netlist
- Recognize the behaviour of the circuit
- Read the sub circuit
- Attach the neccessary power sources
- Apply stimulus
- Give values for load capacitance
- Provide neccessary simulation commands (.tran, .op etc)


------


## Day_19

**16 mask CMOS process**

- Selecting a substrate

- Creating active region for transistors

- P well and N well formation

- Formation of gate

- Lightly doped drain formation
  * Hot electron effect --> high enery carriers break Si-Si bonds.
  * Short channel effect

- Source drain formation

- Formation of contacts and interconnects (local)

- High level metal layer formation

**Notes:**
- From the substrate to the final metal layer a total of 16 masks are used for photolithography.
- The process of growing field oxide is known as LOCOS (local oxidation of Si).
- To form any p+/n+ region, the area is doped with either B/P respectively using a process known as ion implantation.
- Plasma anisotropic etching is done in LDD stage to create side wall spaces next to gate.


**Layout schematic in magic of inverter cell**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/1a56f6c6-3d36-4189-b3c9-46778b2e14c3)

**Extracted spice netlist from the inverter layout**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/9c831389-77ae-4ed7-b227-6dbb0cb7ad7f)


**Spice simulation output**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/01b61f39-603d-415b-8ba1-1c6bfe5f0f1b)

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/600670f2-ac42-424d-a751-3694776b5a77)


------


## Day_20

**Important guidelines:**

- Input and output ports must lie on the intersection of the horizontal and vertical tracks.
- Width of the standard cell should be in odd multiples of the track pitch.
- Height should be in odd multiples of vertical pitch.
- Routes are specified by the tracks it can take.

**It can be observed from the below figure that the input A and output Y lie on intersection of horizontal and vertical track**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/e8ca5ea6-6218-47d6-8ea5-30b0299b9ca5)

~~~
magic -T sky130A.tech sky130_inv.mag &

In command window of magic:
% grid <horizontal and vertical pitch values>
~~~

**LEF file extraction from sky130_vsdinv.mag**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/3cd7dc0d-f71c-4776-9a5f-649717dd38d8)

**LEF file snippet with port parameters for inverter**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/9e0c0ac8-3612-4f41-864d-4c60907e24e6)

**Modified config.tcl file to include vsd_inverter custom standard cell**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/edeeb5d2-97e5-4bd2-b301-52de4e5b725c)


**The characterized vsd_inverter lef file merged and synthesized**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/20aacbfd-f493-48b5-bd9d-90dd5f621427)

- It can be observed that there are 1554 custom inverter instances

**Viewing the placement of sky130_vsdinv in magic**

![image](https://github.com/rakshith0609/rakshith-vsd_hdp/assets/112770970/60d6cc93-d20b-4c47-8e72-9a04550ca175)









