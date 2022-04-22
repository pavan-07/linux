# CMPE 283 Assignment 1
Team Member: Wang, Qin  
Student ID : 013986752  

## Question: Describe in detail the steps you used to complete the assignment.
## Answer:
Assignment 1 is to create a Linux kernel module that will query various MSRs to determine
virtualization features available in our CPU. This module will report (via the system message log) the
features it discovers.

Prerequisites:
• A machine capable of running Linux, with VMX virtualization features exposed.

Implementation steps:
1. Install Oracle VM VirtualBox and Ubuntu    

2. Download the Linux kernel source code:  
   Install git: sudo apt-get install git  
   Fork from https://github.com/torvalds/linux.git to my repositories https://github.com/Qinwang1993/linux  
   git clone https://github.com/Qinwang1993/linux  

3. Follow the instructions https://wiki.ubuntu.com/Kernel/BuildYourOwnKernel to build the environment:   
   sudo apt-get build-dep linux linux-image-$(uname -r)  
   libncurses-dev gawk flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf  
 

4. Modify the .c file that will be used to find the capabilities of the MSRs:  
   Code is shown as: https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_1/cmpe283-1.c  

5. Creating new kernel module for MSRs:  
   - make

6. Inserting/Loading the specific kernel module into the kernel:  
   - sudo insmod ./cmpe283-1.ko

7. Output from the kernel in the system message log:
   - dmesg

The output log displayed in the appendix of this file. https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_1/output
