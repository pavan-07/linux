# CMPE 283 Assignment 2  
Team Member: 
Qin Wang - 013986752    
Chen Zhang - 014536496  

## Assignment 2:  
This assignment focuses on modifying processor instruction behavior inside the KVM hypervisor.   
We need to modify the CPUID emulation code in KVM to report back additional information when a special CPUID “leaf function” is called.  
• For CPUID leaf function %eax=0x4FFFFFFF:  
• Return the total number of exits (all types) in %eax  
• Return the high 32 bits of the total time spent processing all exits in %ebx  
• Return the low 32 bits of the total time spent processing all exits in %ecx  
• %ebx and %ecx return values are measured in processor cycles  

## Question: 
### 1. For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched. 
### Answer:
We met and did this research together. The following steps were all discussed and completed by ourselves:  
• Revisited the related video lecture and the requirements of assignment2  
• Code cupid.c, vmx.c and test.c modules  
• Created nested VM to run the test program  
• Finish the report  

### 2. Describe in detail the steps you used to complete the assignment. 
### Answer:
#### Initial Setup
1. Build environment https://wiki.ubuntu.com/Kernel/BuildYourOwnKernel  
2. Clone the Kernel code from GitHub: git clone https://github.com/torvalds/linux.git  
3. Kernel Code Compilation :  
   uname -a  
   cp /boot/config-5.8.0-43-generic ./.config  
   make oldconfig  
   make -j 2 modules && make -j 2 && sudo make modules_install && sudo make install  
   reboot  
   Verify the updated Linux version: uname -a  
#### Build
1.Modify cpuid.c and vmx.c  
2.Compile using: make -j 2 modules && make -j 2 && sudo make modules_install && sudo make install  
#### Setup KVM
1.Install KVM and supporting packages: sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils  
2.Install the virt-manager using: sudo apt-get install virt-manager  
3.Reboot  
 
#### Created nested VM
1.Use virt-manager to create nested virtual machine  
2.Install Ubuntu in nested VM  
 
#### Test  
1. Write test.c  
2.Install gcc https://linuxize.com/post/how-to-install-gcc-compiler-on-ubuntu-18-04/  
3.Compile test file: gcc test.c  
4.Check output  
<div  align="center">    
   <img src = "https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_2/Picture1.png" width = "700" />
</div>
5.Check host VM kern.log: tail -n20 /var/log/kern.log  
 <div  align="center">    
   <img src = "https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_2/Picture2.png" width = "700" />
</div>
 

### 3. Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?
### Answer:
No, the number of exits increase at unstable rate. There are other VM instructions/operations, so exits are executed, such as EPT violation, RDRAND, I/O instructions, RDTSCP, etc. The number of exits after the first build, rebooting and using KVM to enter the nested VM was 156,411. This may not be very accurate, because there may be a shutdown time with a hardware interruption in between.
