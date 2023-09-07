VLSI Physical Design for ASICs


Objective


ASIC design is a methodology of cost and size reduction of an electronic circuit, product or system through miniaturization and integration of individual components and their functionality into a single element – an Application Specific Integrated Circuit (ASIC).


vlsi design flow:

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/71cfc73e-749f-435b-8054-12f9e58d8afb)

Step 1. Chip Specification
Step 2. Design Entry / Functional Verification
Step 3. RTL block synthesis / RTL Function
Step 4. Chip Partitioning
Step 5. Design for Test (DFT) Insertion
Step 6. Floor Planning (blueprint your chip)
Step 7. Placement
Step 8. Clock tree synthesis
Step 9. Routing
Step 10. Final Verification (Physical Verification and Timing)




    



INSTALLATIONS:

1. ubuntu

2. neccesaries for risc v toolchain:

sudo apt-get install git vim -y
sudo apt-get install autoconf automake autotools-dev curl libmpc-dev         libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo     gperf libtool patchutils bc zlib1g-dev git libexpat1-dev gtkwave -y
cd
pwd=$PWD
mkdir riscv_toolchain
cd riscv_toolchain
wget "https://static.dev.sifive.com/dev-tools/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14.tar.gz"
tar -xvzf riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14.tar.gz 
export PATH=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH
sudo apt-get install device-tree-compiler -y
git clone https://github.com/riscv/riscv-isa-sim.git
cd riscv-isa-sim/
mkdir build
cd build
../configure --prefix=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14
make
sudo make install
cd $pwd/riscv_toolchain
git clone https://github.com/riscv/riscv-pk.git
cd riscv-pk/
mkdir build
cd build/
../configure --prefix=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14 --host=riscv64-unknown-elf
make
sudo make install
export PATH=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf/bin:$PATH
cd $pwd/riscv_toolchain
git clone https://github.com/steveicarus/iverilog.git
cd iverilog/
git checkout --track -b v10-branch origin/v10-branch
git pull 
chmod 777 autoconf.sh 
./autoconf.sh 
./configure 
make
sudo make install 



DAY -1:

Labwork for RISCV Toolchain:



LAB 1:



C Program

We wrote a C program for calculating the sum from 1 to n using a text editor, leafpad.


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/f1b66028-3d31-4f26-ae4f-1d48e21d577f)
#include<stdio.h>





int main(){
	int i, sum=0, n=111;
	for (i=1;i<=n; ++i) {
	sum +=i;
	}
	printf("Sum of numbers from 1 to %d is %d \n",n,sum);
	return 0;
}

risc v gnu toolchain:

RISC-V GNU Compiler Toolchain. This is the RISC-V C and C++ cross-compiler. It supports two build modes: a generic ELF/Newlib toolchain and a more sophisticated Linux-ELF/glibc toolchain.
GNU == gnu's NOT UNIX.




NOW, WE RUN THE SAME USING RISC V GCC COMPILER:





running of spike commands


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/ed2cbcd6-fe10-4a4e-b8a8-f2f851a1d99d)


ABOUT SPIKE:

Spike is the golden reference functional RISC-V ISA C++ sofware simulator. It provides full system emulation or proxied emulation with HTIF/FESVR. 
    

running of signed and unsigned numbers


The key difference between unsigned and signed in our context is what happens when you assign an (unsigned) byte to an integer. If a signed byte is assigned, then the resulting integer is sign extended (i.e., 0xff becomes 0xffffffff).


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/4b6d7c4f-c309-4808-b61c-c0621c3e0a6f)


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/419d8786-6524-4b00-a5d1-b8085f88e898)



DAY -2:

Labwork using ABI Function Calls:



    An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures.
    The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.




LAB 2 :


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/c6419305-45b5-460e-a093-99b92258b96e)



![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/e3737755-48da-4121-a1b7-efd408b4241a)



![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/2652903b-9823-4c1e-a7eb-f98d9e4e3bcf)





DAY -3:

Introduction to verilog RTL design and synthesis:

RTL is an acronym for register transfer level. This implies that your Verilog code describes how data is transformed as it is passed from register to register.



Introduction to Open-Source Simulator iVerilog:

simulator:

It is used for checking our RTL design .
The tool used in this process in iverilog.
simulator changes its output as the input changes.


design:

design is a set of verilog codes for meeting our requirements.

testbench:

this used for verifying and testing if our design is meeting the required specifications.

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/1ad8eafc-61a3-41d3-adfd-c01e02716053)

we observe here that,there are no primary inputs and primary outputs.


stimulus:
it uses test vectors for verfying the output for a given input.







INTRODUCTION TO YOSYS:


Yosys is a framework for RTL synthesis and more. It currently has extensive Verilog-2005 support and provides a basic set of synthesis algorithms for various application domains. Yosys is the core component of most our implementation and verification flows.

it is a synthesizer: hence converts the RTL TO NETLIST.


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/17bf9ab1-571b-4f2e-8880-20e852a7b338)


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/4cdbb7c5-ef21-4ed5-8e2f-2889ab600d74)




.lib is collection of logical modules that include (standard cells) various gates of different flavours:(fast,slow,medium)

faster cells: require more current for charging and discharging of capacitors,hence the power and area that is width are compromised.
slower cells: they cause sluggish performance.
hence we can also use medium cells.



LAB - 3:



Commands used to perform different opertions:

 
   1.read_verilog to read the design
   2.read_liberty to read the .lib file
   3.write_verilog to write out the netlist file
   4.show to open the netlist viewer.
   5.To read the library
   6.read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   7.To read the design
   8.read_verilog good_mux.v
   9.To syntheis the module
   10.synth -top good_mux
   11.to generate the netlist
   12.abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   13.To write the netlist
   14.write_verilog good_mux_netlist.v
   15.!gvim good_mux_netlist.v
   16.To view a simplified code
   17.write_verilog -noattr good_mux_netlist.v
   18.!gvim good_mux_netlist.v




i) yosys package:

        cd
        cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
        Type yosys



1.
    ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/565a7534-ccfe-452e-9de3-826f67e0e5b9)


2.
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/20e8526b-358f-4ca0-866d-8a5c0ebb0024)






ii) for a 2:1 mux:



Yosys good_mux:

1) ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/4b800495-0a82-40c9-b443-e15f4d2c053a)



3) ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/0d5777eb-8529-49e5-9861-786ba27052c0)


    
    
    
iii) netlist creation:

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/7e476f7c-d334-41d8-ad19-2c7940c0960f)






iv) installing vim:


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/ae3b13ce-762b-4cc4-aaa3-327e021a374e)


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/be736300-6ab1-429e-b5f9-81a004de718b)



v) after switching, the extra info is dumped out hence we obtain:

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/95daa6fd-8855-4699-ae7d-d884c878a3c6)



LAB -4 :

Introduction to Timing Dot Libs:



    The first line in the file library ("sky130_fd_sc_hd__tt_025C_1v80") :
    
        tt : indicates variations due to process and here it indicates Typical Process.
	
        025C : indicates the variations due to temperatures where the silicon will be used.
	
        1v80 : indicates the variations due to the voltage levels where the silicon will be incorporated.


 ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/2ecac063-6427-49c5-96b1-3e05a7738a0b)

 Hierarchical vs Flat Synthesis:
 

Hierarchical Synthesis Hierarchical synthesis is an approach in digital design and logic synthesis where complex designs are broken down into smaller, more manageable modules or sub-circuits, and each module is synthesized individually. These synthesized modules are then integrated back into the overall design hierarchy. This approach helps manage the complexity of large designs and allows designers to work on different parts of the design independently.


![Screenshot from 2023-08-30 23-04-51](https://github.com/ughdeiek/pes_asic_class/assets/142580251/de8506f0-c6d8-4133-9842-ce2eb436982e)




    multiple_modules instantiates sub_module1 and sub_module2

    Launch yosys

    read the library file read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

    read the verilog file  read_verilog multiple_modules.v

    synth -top multiple_modules to set it as top module

![Screenshot from 2023-08-30 23-04-51](https://github.com/ughdeiek/pes_asic_class/assets/142580251/13524cd2-fcdb-4f54-878a-669c322ce35a)

![Screenshot from 2023-08-30 23-37-43](https://github.com/ughdeiek/pes_asic_class/assets/142580251/0da09c02-ce9b-48dc-a301-bba9cf86403e)

![Screenshot from 2023-08-31 00-05-43](https://github.com/ughdeiek/pes_asic_class/assets/142580251/7b1d77e6-f2e7-4684-a4d5-442fcbc257a4)




abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

To view the netlist show multiple_modules

![Screenshot from 2023-08-30 23-39-13](https://github.com/ughdeiek/pes_asic_class/assets/142580251/4d79be56-e4e7-4753-8518-397dd3fd46e3)



    Here it shows sub_module1 and sub_module2 instead of AND gate and OR gate.

    write_verilog -noattr multiple_modules_hier.v
    !gvim multiple_modules_hier.v

    
    ![Screenshot from 2023-08-30 23-52-22](https://github.com/ughdeiek/pes_asic_class/assets/142580251/cf6abf7a-79a0-414b-9f55-5a6f32ff2a03)

    ![Screenshot from 2023-08-31 00-06-50](https://github.com/ughdeiek/pes_asic_class/assets/142580251/b639970e-0037-4233-a536-1e0249587605)

    
Flattened Synthesis Flattened synthesis is the opposite of hierarchical synthesis. Instead of maintaining the hierarchical structure of the design during synthesis, flattened synthesis combines all modules and sub-modules into a single, flat representation. This means that the entire design is synthesized as a single unit, without preserving the modular organization present in the original high-level description.

    Launch yosys
    read the library file read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    read the verilog file  read_verilog multiple_modules.v
    synth -top multiple_modules to set it as top module
    abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    flatten to write out a flattened netlist
    show

    
    write_verilog -noattr multiple_modules_flat.v
    !gvim multiple_modules_flat.v


![Screenshot from 2023-08-30 23-58-14](https://github.com/ughdeiek/pes_asic_class/assets/142580251/e9e2d16e-30f7-4d97-a678-243724c0e689)



Various Flop Coding Styles and Optimization:


    A flip-flop (often abbreviated as "flop") is a fundamental building block in digital circuit design.
    It's a type of sequential logic element that stores binary information (0 or 1) and can change its output based on clock signals and input values.
    In a combinational circuit, the output changes after the propagation delay of the circuit once inputs are changed.
    During the propagation of data, if there are different paths with different propagation delays, then a glitch might occur.
    There will be multiple glitches for multiple combinational circuits.
    Hence, we need flops to store the data from the combinational circuits.
    When a flop is used, the output of combinational circuit is stored in it and it is propagated only at the posedge or negedge of the clock so that the next combinational circuit gets a glitch free input thereby stabilising the output.
    We use control pins like set and reset to initialise the flops.
    They can be synchronous and asynchronous.

D Flip-Flop with Asynchronous Reset

    When the reset is high, the output of the flip-flop is forced to 0, irrespective of the clock signal.
    Else, on the positive edge of the clock, the stored value is updated at the output.


    
    cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
    iverilog dff_async_set.v tb_dff_async_set.v
    ./a.out
    gtkwave tb_dff_async_set.vcd



    Synthesis
        cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
        yosys
        read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
        read_verilog dff_async_set.v
        synth -top dff_async_set
        dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
        abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
        show


![Screenshot from 2023-09-03 15-43-35](https://github.com/ughdeiek/pes_asic_class/assets/142580251/8366c764-4615-4321-8507-6e6f78a4bfe3)


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/f0c37a52-d69c-4fd7-93f9-b7a96d65a5f7)

![Screenshot from 2023-09-03 15-22-45](https://github.com/ughdeiek/pes_asic_class/assets/142580251/e020dffe-e2d0-45ad-bd31-27c6fca7cb3c)

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/fd6bb63d-4ce1-4d9c-90a1-00c16c52ea3e)



D Flip-Flop with Synchronous Reset

    Simulation
        cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
        iverilog dff_syncres.v tb_dff_syncres.v
        ./a.out
        gtkwave tb_dff_syncres.vcd

![Screenshot from 2023-09-03 15-32-00](https://github.com/ughdeiek/pes_asic_class/assets/142580251/2b6db40c-6596-43af-b351-e972bfa4cb47)




Synthesis

    cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
    yosys
    read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    read_verilog dff_syncres.v
    synth -top dff_syncres
    dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
    abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    show

    ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/4ae2fd7d-ea63-432b-825d-c4b0f02ce5b7)

Some more optimizations: 


    gvim mult_2.v

image

    read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    read_verilog mult_2.v
    synth -top mul2

image

    abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    show

image

    write_verilog -noattr mul2_netlist.v
    !gvim mul2_netlist.v

image



    gvim mult_8.v
    image

    read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  

    read_verilog mult_8.v

    synth -top mult8

image

    abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    show

image


    write_verilog -noattr mult8_netlist.v
    !gvim mult8_netlist.v

image















    






    


    



    

    

























