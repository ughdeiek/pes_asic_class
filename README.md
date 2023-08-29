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

1. ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/c30aa54a-cd02-4240-ad10-a9b839f92913)

2. ![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/565a7534-ccfe-452e-9de3-826f67e0e5b9)


3.
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



v) after switching the extra info is dumped out hence we obtain:

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/95daa6fd-8855-4699-ae7d-d884c878a3c6)


    






    


    



    

    

























