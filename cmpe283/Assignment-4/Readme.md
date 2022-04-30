# CMPE 283 Assignment 4  
Name: Pavan Badarinath
Stduent ID: 014499225

## Assignment 4:  
This assignment is to illustrate the difference in performance when using nested paging versus shadow paging, and to illustrate the different exit frequencies and types.   

## Question: 

### 2. Include a sample of your print of exit count output from dmesg from “with ept” and “without ept”.
 The output are displayed in the appendix of this file.  
 see:
 https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_4/assignment4_nested.txt
 https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_4/assignment4_shadow.txt
 
### 3. What did you learn from the count of exits? Was the count what you expected? If not, why not?
# Answer
The count of exits is less in nested paging and more in shadow paging.
The count was expected because in nested paging, there are two page tables, a guest page table and a host page table. There is also an extra file called TAG in the TLB, which indicates whether it's a host table or a guest table entry. There is also a field for PID that the hypervisor can refer to when it needs to clear the TLB for a specific VM process when it context switches inside the VM. Having a nested page table means that more memory locations (for instructions and their addresses) can be accessed in the 4-level page table, so the number of exits has been minimized, the number of memory accesses is higher than that of shadow paging. However, there are many processor caches that can alleviate this situation, and intel and amd no longer improve shadow paging.
- If the VM moves from a nested page to a shadow page, the shadow page table will be managed by the VMM. In the shadow page, CR3 points to the shadow page table of the hypervisor that needs to exit the #PF page fault. Therefore, when the VM checks the page, it will not find the page in the guest page table, and the hypervisor needs to copy the page. The entries of the shadow page table and TLB will also be filled. However, to deal with the issue of memory release, we also need to enable the TLB refresh exit function so that the shadow table can be synchronized and updated. Therefore, shadow paging increases the number of exits, and compared with nested paging, the implementation of shadow paging is considered complicated.

### 4. What changed between the two runs (ept vs no-ept)?
# Answer 
When you compare the nested paging (with ept) with nested paging (no-ept), the number of exits for shadow paging keeps increasing.
