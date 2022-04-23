CMPE 283 Assignment 1
Name: Pavan Badarinath 
Student ID : 014499225  

# Question: Describe in detail the steps you used to complete the assignment.
# Answer:
In this assignment we need to create a Linux kernel module that will query multiple MSRs to determine various
virtualization features that is available in our CPU. This module will report all different kinds of
features it discovers through a system message log.

# Implementation steps:
1. Install Oracle VM VirtualBox and select Ubuntu.  

2. Download the Linux kernel source code:  
   Install git: sudo apt-get install git  
   Fork from https://github.com/torvalds/linux.git to my repositories https://github.com/pavan-07/linux
   git clone https://github.com/pavan-07/linux  

3. Follow the instructions https://wiki.ubuntu.com/Kernel/BuildYourOwnKernel to build the environment:   
   sudo apt-get build-dep linux linux-image-$(uname -r)  
   libncurses-dev gawk flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf  
 
4. Modify the .c file that will be used to find the capabilities of the MSRs:  
   Code is shown as: https://github.com/pavan-07/linux/blob/master/cmpe283/Assignment_1/cmpe283-1.c  

5. Creating new kernel module for MSRs:  
   - make

6. Inserting/Loading the specific kernel module into the kernel:  
   - sudo insmod ./cmpe283-1.ko

7. Output from the kernel in the system message log:
   - dmesg

