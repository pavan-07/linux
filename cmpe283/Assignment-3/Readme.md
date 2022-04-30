This assignment focuses on modifying the CPUID emulation code in KVM to report back additional information when special CPUID leaf nodes are requested.

• For CPUID leaf node %eax=0x4FFFFFFE:  
• Return the number of exits for the exit number provided (on input) in %ecx  
• This value should be returned in %eax  

For leaf nodes 0x4FFFFFFE, if %ecx (on input) contains a value not defined by the SDM, return 0 in all %eax, %ebx, %ecx registers and return 0xFFFFFFFF in %edx. For exit types not enabled in KVM, return 0s in all four registers. At a high level, we will need to perform the following:

• Start with our assignment 2 environment  
• Modify the kernel code with the assignment functionality:   
• Create a user-mode program that performs various CPUID instructions required to test the assignment  
• Verify proper output  

## Question: 
### 1. For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched. 
### Answer:
We met and did this research together. The following steps were all discussed and completed by ourselves:  
• Reuse the assignment2 environment  
• Revisited the related video lecture and the requirements of assignment3  
• Code cupid.c, vmx.c files  
• Run the test_assignment3.c in the nested VM and get the result  
• Discuss the questions and finish the report  

### 2. Describe in detail the steps you used to complete the assignment. Consider your reader to be someone skilled in software development but otherwise unfamiliar with the assignment. Good answers to this question will be recipes that someone can follow to reproduce your development steps.
### Answer:
#### Initial Setup
Reuse the assignment2 environment: https://github.com/Qinwang1993/CMPE-283/tree/master/Assignment_2
#### Build
1.Modify cpuid.c and vmx.c files
![image](https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_3/Modify%20the%20code%20at%20the%20end%20of%20the%20cpuid.c%20file%20.png)
2.Compile using: make -j 4 modules && make -j 4 && sudo make modules_install && sudo make install

3.reboot

# 2. Describe in detail the steps you used to complete the assignment.  
Answer:
# Initial Setup:
1. Build environment https://wiki.ubuntu.com/Kernel/BuildYourOwnKernel  
2. Clone the Kernel code from GitHub: git clone https://github.com/torvalds/linux.git  
3. Kernel Code Compilation :  
   uname -a  
   cp /boot/config-5.8.0-43-generic ./.config  
   make oldconfig  
   make -j 2 modules && make -j 2 && sudo make modules_install && sudo make install  
   reboot  
   Verify the updated Linux version: uname -a  
# Build
1.Modify cpuid.c and vmx.c  
2.Compile using: make -j 2 modules && make -j 2 && sudo make modules_install && sudo make install  
# Setup KVM
1.Install KVM and supporting packages: 
sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils  
2.Install the virt-manager using: 
sudo apt-get install virt-manager  
3.Reboot  
 
# Created nested VM
1.Use virt-manager to create nested virtual machine  
2.Install Ubuntu in nested VM  
 
# Test  
1. Write test.c  
2.Install gcc https://linuxize.com/post/how-to-install-gcc-compiler-on-ubuntu-18-04/  
3.Compile test file: gcc test.c  
4.Check output  
#### Test
Start the nested VM and verify CPUID exit conditions using the test_assignment3.c file.
1. First run: result detail at :https://github.com/pavan-07/linux/blob/master/cmpe283/Assignment-3/first_run.txt

2. Second run: result detail at : https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_3/second_run.txt


### 3. Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?
### Answer:
The result of the first run and second run shows that the number of exits does not increase at stale rate. Many operations like External Interrupt, I/O instruction etc., will cause more exits of around 1,400, 000.

### 4. Of the exit types defined in the SDM, which are the most frequent? Least?
### Answer:
The most frequent exit types are: External Interrupt, cpuid, I/O instrcution.
The least frequent exit types are: And MOV DR, INVD.


