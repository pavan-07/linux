CMPE 283 Assignment 2  
Name: Pavan Badarinath
# Student ID: 014499225 

Questions: 

2. Describe in detail the steps you used to complete the assignment.  
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
 

3. Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?
Answer:
No, the number of exits does not increase at stable rate. There are other VM instructions, so exits are performed during certain VM operations, such as RDRAND, EPT violation, RDTSCP, I/O instructions,  etc. The total number of exits was approximately 156,345.
