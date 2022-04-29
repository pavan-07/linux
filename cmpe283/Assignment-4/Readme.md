# CMPE 283 Assignment 4  


## Assignment 4:  
This assignment is to illustrate the difference in performance when using nested paging versus shadow paging, and to illustrate the different exit frequencies and types.   

## Question: 
### 1. For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched. 
### Answer:
We met and did this research together. The following steps were all discussed and completed by ourselves:  
1. Test nested paging  
  Boost nested VM  
  Run test_assignment3.c in nested VM  
  Paste result in assignment4_nested.txt  
  Shut down nested VM  
  ![image](https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_4/Picture1.png)
2. Test shadow paging
  Remove kvm-intel module from your running kernel
  sudo rmmod kvm-intel
  Reload kvm-intel module with the parameter ept=0
  Sudo insmod /lib/modules/5.12.0+/kernel/arch/x86/kvm/kvm-intel.ko ept=0
   ![image](https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_4/Picture2.png)
3. Boost the same nested VM
4. Run test_assignment3.c in nested VM
5. Paste result in assignment4_shadow.txt
6. Shut down nested VM

### 2. Include a sample of your print of exit count output from dmesg from “with ept” and “without ept”.
 The output are displayed in the appendix of this file.  
 see:
 https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_4/assignment4_nested.txt
 https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_4/assignment4_shadow.txt
 
### 3. What did you learn from the count of exits? Was the count what you expected? If not, why not?
The count of number of exits is less in nested paging and more in shadow paging.
The count was expected because:
- In nested paging,there are two page tables, guest page table and host page table. There will be an additional file called TAG in the TLB, which will indicate whether it is a host table or a guest table entry. There will also be field for PID that the hypervisor can refer when it needs to clear the TLB for a specific VM process when it context switches inside the VM. Having a nested page table means that more memory locations (for instructions and their addresses) can be accessed in the 4-level page table, so the number of exits has been minimized, the number of memory accesses is higher than that of shadow paging. However, there are many processor caches that can alleviate this situation, and intel and amd no longer improve shadow paging.
- If the VM moves from a nested page to a shadow page, the shadow page table will be managed by the VMM. In the shadow page, CR3 points to the shadow page table of the hypervisor that needs to exit the #PF page fault. Therefore, when the VM checks the page, it will not find the page in the guest page table, and the hypervisor needs to copy the page. The entries of the shadow page table and TLB will also be filled. However, to deal with the issue of memory release, we also need to enable the TLB refresh exit function so that the shadow table can be synchronized and updated. Therefore, shadow paging increases the number of exits, and compared with nested paging, the implementation of shadow paging is considered complicated.

### 4. What changed between the two runs (ept vs no-ept)?
Compared with the nested paging (with ept), the number of exits for shadow paging (without ept) keeps increasing.
