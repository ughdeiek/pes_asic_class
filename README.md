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



![Screenshot from 2023-09-07 23-09-13](https://github.com/ughdeiek/pes_asic_class/assets/142580251/6afbc915-2ed4-40ff-8104-8c12ad6ff1f9)






Lab to Run C-Program on RICV-CPU :

![Screenshot from 2023-09-07 23-15-09](https://github.com/ughdeiek/pes_asic_class/assets/142580251/6968e34e-c53f-4c85-8498-6d121a75f392)


![Screenshot from 2023-09-07 23-15-22](https://github.com/ughdeiek/pes_asic_class/assets/142580251/43c1c1b4-0525-4eb5-808a-2fe2457ad0ac)






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



DAY -4:

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

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/0662241d-070a-4ea4-8afb-1524c262b02b)


    read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    read_verilog mult_2.v
    synth -top mul2
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/ed863a9f-bb38-4081-8944-e6248c61c147)


    abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    show

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/8a9773e2-27cb-418d-8783-70ed43d4938f)


    write_verilog -noattr mul2_netlist.v
    !gvim mul2_netlist.v
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/36e54291-f70a-43b3-a9be-6e907fca1f1d)




    gvim mult_8.v
    
    ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/30feffe5-25c6-4647-a1be-b176d29a1299)

    read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  

    read_verilog mult_8.v

    synth -top mult8

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/fa90dbbc-b8c1-4808-9350-5b9023221f4b)


    abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    show

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/66f491c6-115d-461b-aeff-b20e820942a7)



    write_verilog -noattr mult8_netlist.v
    !gvim mult8_netlist.v

    ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/65c71706-8f0a-44a3-8ad7-899d3fa97906)




    DAY -5 

    LAB-5:

    Introduction to OptimisationS:

    Combinational Logic Optimisations
opt_check

    gvim opt_check.v

    ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/f7d17297-467a-450f-b600-fc058a487cbb)

    

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

read_verilog opt_check.v

synth -top opt_check

opt_clean -purge

abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

show

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/ebd6a1e3-21db-4976-bbef-956acf018e2d)

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/a9c66c75-9b3f-4534-87ef-a00588e21944)

 opt_check2

    gvim opt_check2.v

    ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/e4a6bd10-4ccf-4874-8020-612f24fe49e4)


read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

read_verilog opt_check2.v

synth -top opt_check2

opt_clean -purge

abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

show
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/a85db574-7c23-440e-8371-be22de5e32b1)

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/ab32a822-2d13-44b1-95e1-27152a6423ac)


    gvim opt_check3.v

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/357c9863-9818-473d-9e92-39b09207dead)


    read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    read_verilog opt_check3.v
    synth -top opt_check3
    opt_clean -purge
    abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    show

    ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/b5d0bcc2-3a71-4d98-a81d-932dff70c641)

    ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/c0363c73-4784-4b92-9a63-9a231290c143)



    gvim opt_check4.v

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/7fd34916-22ff-4669-8e7d-96709ba66e70)

    read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    read_verilog opt_check4.v
    synth -top opt_check4
    opt_clean -purge
    abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    show

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/89ffca85-2505-40e4-b179-1b8da3961031)

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/8d45e90b-bfd9-4b7a-8bf2-65423de9dcc8)


 multiple_module_opt

    gvim multiple_module_opt.v

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/b4e667cd-8454-4bed-9ea7-40085238ceb7)


    read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    read_verilog multiple_module_opt.v
    synth -top multiple_module_opt
    opt_clean -purge
    abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    show

    ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/768fcdad-6ac9-406b-8cef-1155468a3733)

    ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/e0c6edb5-6a37-485f-9eeb-5bb49336dca4)


 
    
    
 Sequential Logic Optimisations:





dff_const1
gvim dff_const1.v
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/34486ba8-0c89-4e30-a424-1aefd062e620)

Simulation

iverilog dff_const1.v tb_dff_const1.v
/a.out
gtkwave tb_dff_const1.vcd


Synthesis

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const1.v
synth -top dff_const1
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/ed864f03-f141-4f9f-bd31-9e726f1faaa5)
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/c6490d7a-9398-4f73-922f-0bb9cd557474)






 
dff_const2
gvim dff_const2.v

Simulation

iverilog dff_const2.v tb_dff_const2.v
/a.out
gtkwave tb_dff_const2.vcd
Screenshot from 2023-08-29 07-47-58

Synthesis

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const2.v
synth -top dff_const2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/ffe58a8a-f1a1-4ea0-938e-d4e49628bf2e)

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/74a8ac0c-cdff-4abf-b825-ba677cc075f2)








gvim dff_const3.v

Simulation

iverilog dff_const3.v tb_dff_const3.v
/a.out
gtkwave tb_dff_const3.vcd

Synthesis

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const3.v
synth -top dff_const3
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/1bdb06f1-d3c7-4153-bda1-219e63d55619)
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/07b9120f-495b-4c3d-a8ae-f0d0844d7fdf)








dff_const4

gvim dff_const4.v

Simulation

iverilog dff_const4.v tb_dff_const4.v
/a.out
gtkwave tb_dff_const4.vcd


Synthesis

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const4.v
synth -top dff_const4
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/1d540bed-3f42-4790-8906-712c09a1fbc1)

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/78926be7-efe4-4115-bb0c-1dfae1c9b7f1)







dff_const5
gvim dff_const5.v

Simulation

iverilog dff_const4.v tb_dff_const4.v
/a.out
gtkwave tb_dff_const5.vcd


Synthesis

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const4.v
synth -top dff_const4
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/c6866b5c-ea52-4c49-b657-f19e3d41f381)
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/46df7dee-1eeb-4123-b195-131bdc43b617)








Sequential Optimisations for Unused Outputs:




counter_opt1
gvim counter_opt.v

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt.v
synth -top counter_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/c6b2fc6a-09f3-4e17-8363-0d1f04abcfc0)

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/3c92f4ba-f128-42bf-911d-ef8da89fc95e)









counter_opt2
gvim counter_opt2.v

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt2.v
synth -top counter_opt2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/b5c28e3f-99a8-49d8-8ce8-8412989db8ed)
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/00520f89-e200-4fe7-b014-6adae6430cc9)


DAY-6:



LAB-6:





GLS Synthesis-Simulation Mismatch and Blocking Non-blocking Statemets:


Gate Level Simualtion
Gate-level simulation is a technique used in digital design and verification to validate the functionality of a digital circuit at the gate-level implementation.
It involves simulating the circuit using the actual logic gates and flip-flops that make up the design, as opposed to higher-level abstractions like RTL (Register Transfer Level) descriptions.
This type of simulation is typically performed after the logic synthesis process, where a high-level description of the design is transformed into a netlist of gates and flip-flops.




Synthesis-Simulation Mismatch

A synthesis-simulation mismatch refers to a situation in digital design where the behavior of a circuit, as observed during simulation, doesn't match the expected or desired behavior of the circuit after it has been synthesized.
This discrepancy can occur due to various reasons, such as timing issues, optimization conflicts, and differences in modeling between the simulation and synthesis tools.
This mismatch is a critical concern in digital design because it indicates that the actual hardware implementation might not perform as expected, potentially leading to functional or timing failures in the fabricated chip.





Blocking Statements

Blocking statements are executed sequentially in the order they appear in the code and have an immediate effect on signal assignments.

Non-Blocking Statements

Non-blocking assignments are used to model concurrent signal updates, where all assignments are evaluated simultaneously and then scheduled to be updated at the end of the time step.

Caveats with Blocking Statements

Blocking statements in hardware description languages like Verilog have their uses, but there are certain caveats and considerations to be aware of when working with them. 


Labs on GLS and Synthesis-Simulation Mismatch:





ternary_operator_mux



gvim teranry_operator_mux.v




Simulation

iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd

![Screenshot from 2023-09-07 21-57-45](https://github.com/ughdeiek/pes_asic_class/assets/142580251/b6f45d25-f3ba-41ea-87c2-e3ff33de8e67)

![Screenshot from 2023-09-07 21-59-40](https://github.com/ughdeiek/pes_asic_class/assets/142580251/6703bd3d-7145-4585-8a53-a88ecc274677)

![Screenshot from 2023-09-07 22-02-35](https://github.com/ughdeiek/pes_asic_class/assets/142580251/bb2a7e8f-daa0-4bb0-b3f1-315f8617c2c5)

![Screenshot from 2023-09-07 22-03-03](https://github.com/ughdeiek/pes_asic_class/assets/142580251/2c368198-adea-4c6c-8985-aae12c815b07)





Synthesis


read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog ternary_operator_mux.v
synth -top ternary_operator_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/2ebc5275-9b5a-49ff-9f27-89e26cd80d59)


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/90bdfe6a-621f-4d56-9c7b-49c084760c64)




GLS to Gate-Level Simulation



iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
./a.out


gtkwave tb_bad_mux.vcd

![Screenshot from 2023-09-07 22-36-43](https://github.com/ughdeiek/pes_asic_class/assets/142580251/0861dd40-e203-4e43-aedc-2bcff2b5ce9e)

![Screenshot from 2023-09-07 22-40-07](https://github.com/ughdeiek/pes_asic_class/assets/142580251/ca8b8c07-e305-44fa-b6a7-92cf4321a74f)




gvim bad_mux.v





Simualtion

iverilog bad_mux.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd

![Screenshot from 2023-09-07 22-24-19](https://github.com/ughdeiek/pes_asic_class/assets/142580251/310348a1-6e17-4640-97a0-1d8a27fb1b21)




Synthesis


read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog bad_mux.v
synth -top bad_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/b8e74627-13a8-4499-8372-29225bd4fca4)


![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/7d7a9304-180e-408c-b2f5-efedf2a1839e)





GLS to Gate-Level Simulation



iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd

![Screenshot from 2023-09-07 22-24-19](https://github.com/ughdeiek/pes_asic_class/assets/142580251/e7443f13-4d21-48b1-90f4-86100343cab7)

![Screenshot from 2023-09-07 22-24-10](https://github.com/ughdeiek/pes_asic_class/assets/142580251/293d7116-b56d-41b4-85f4-ac56767d8719)




Labs on Synth-Sim Mismatch for Blocking Statement:

blocking_caveat



gvim blocking_caveat.v

Simualtion

iverilog blocking_caveat.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd

![Screenshot from 2023-09-07 22-24-19](https://github.com/ughdeiek/pes_asic_class/assets/142580251/4898de89-672c-4b8b-b5e3-c843eabb5f1c)

![Screenshot from 2023-09-07 22-27-35](https://github.com/ughdeiek/pes_asic_class/assets/142580251/8043d138-2239-4254-8307-a8ce2126ef93)

![Screenshot from 2023-09-07 22-29-26](https://github.com/ughdeiek/pes_asic_class/assets/142580251/4f60014a-dc73-473d-8e03-72058ceed222)




Synthesis



read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog blocking_caveat.v
synth -top blocking_caveat
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show

![Screenshot from 2023-09-07 22-29-26](https://github.com/ughdeiek/pes_asic_class/assets/142580251/bdf2b8d3-d459-491f-b545-e6b242bdb2a9)

![Screenshot from 2023-09-07 22-33-20](https://github.com/ughdeiek/pes_asic_class/assets/142580251/4225b8d7-11c1-4274-872d-4feffd15881e)



GLS to Gate-Level Simulation





iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd

![Screenshot from 2023-09-07 22-36-11](https://github.com/ughdeiek/pes_asic_class/assets/142580251/8c6e43de-c081-49b3-b135-e9b2a053d215)

![Screenshot from 2023-09-07 22-36-11](https://github.com/ughdeiek/pes_asic_class/assets/142580251/3d835ce5-d881-4686-85e0-0cc57cf62613)

![Screenshot from 2023-09-07 22-36-43](https://github.com/ughdeiek/pes_asic_class/assets/142580251/e13bf8da-918d-492b-ba17-58e27bfb39c0)

 

















    






    


    



    

    

























