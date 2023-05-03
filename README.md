**A repository with complete documentation of VSD-HDP program**

Program: [SKY130-based ASIC Design Projects](https://www.vlsisystemdesign.com/hdp/)

- Author: T S Rakshith, rakshith.ec20@bmsce.ac.in

Progress Quick-Link:<br />
[Day 1](#Day_1)<br />
[Day 2](#Day_2)<br />
[Day 3](#Day_3)<br />
[Day 4](#Day_4)<br />
[Day 5](#Day_5)<br />
[Day 6](#Day_6)<br />
[Day 7](#Day_7)<br />
[Day 8](#Day_8)<br />
[Day 9](#Day_9)<br />
[Day 10](#Day_10)<br />
[Day 11](#Day_11)<br />
[Day 12](#Day_12)<br />
[Day 13](#Day_13)<br />
[Day 14](#Day_14)<br />
[Day 15](#Day_15)<br />

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


## Day_6

- Design chosen: **8-bit ALU**

- Simulation

![alu sim](https://user-images.githubusercontent.com/112770970/224483732-2948a179-e8ea-4b67-9b1e-b7284c22a2dc.JPG)


- Synthesis

![alu synth](https://user-images.githubusercontent.com/112770970/224483750-733e9c26-dbdf-4df1-a12b-05392c149721.JPG)


- Simulation of gate level netlist (GLS)

![netlist sim alu](https://user-images.githubusercontent.com/112770970/224483778-c4b6d93c-84fc-43c3-847e-0f5739c3d3ce.JPG)

- Design is simulated and synthesized. No simulation-synthesis mismatch is reported.


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



## Day_9

**ALU Constraint file:**

![alu_cons](https://user-images.githubusercontent.com/112770970/230723742-fbdb3c1e-6c46-4a67-9187-de43b2af876a.JPG)


**Timing reports**

![alu_timing1](https://user-images.githubusercontent.com/112770970/230723784-ec4ef32d-40bc-4b6c-878b-a3f4862909df.JPG)

![alu_timing2](https://user-images.githubusercontent.com/112770970/230723790-0dc7a432-f651-448b-8530-3fc7d751aa08.JPG)

![alu_timing3](https://user-images.githubusercontent.com/112770970/232210384-7b617190-19df-4b12-89ad-b234ed5eb27f.JPG)



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



## Day_12

**Spice Netlist for inverter**

![image](https://user-images.githubusercontent.com/112770970/235947980-3f11d4d5-c516-4dab-9b09-72157becbea0.png)


**Spice Simulation of Voltage transfer characteristics of CMOS inverter**

![image](https://user-images.githubusercontent.com/112770970/235947067-113ce1da-5fab-4325-9e6f-4a6b1a797a05.png)

- It can be seen that the switching threshold is around 8.76 V.



## Day_13

**Spice Simulation of Inverter Switching transition**



## Day_14

**Noise Margin**
~~~
    NMH = VOH-VIH // High noise margin
    NML = VIL-VOL // Low noise margin
~~~



## Day_15

**Spice Simulation of Power Supply Scaling**



**Spice Simulation of Device Variation**    
    





