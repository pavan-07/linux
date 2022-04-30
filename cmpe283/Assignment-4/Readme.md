# CMPE 283 Assignment 4  
Name: Pavan Badarinath
Stduent ID: 014499225

## Assignment 4:  
This assignment is to illustrate the difference in performance when using nested paging versus shadow paging, and to illustrate the different exit frequencies and types.   

## Questions: 

### 2. Include a sample of your print of exit count output from dmesg from “with ept” and “without ept”.
 The output are displayed in the appendix of this file.  
 see:
https://github.com/pavan-07/linux/blob/master/cmpe283/Assignment-4/assignment4_nested%5B1%5D.txt
 https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_4/assignment4_shadow.txt
 
### 3. What did you learn from the count of exits? Was the count what you expected? If not, why not?
# Answer:

The number of exits in shadow paging increases compared to nested paging. Yes, the count was expected because, the Nested paging removes the overheads connected with shadow paging. 
The hypervisor does not need to interfere and reproduce the visitor's modification of the guest page table, unlike shadow paging.

### 4. What changed between the two runs (ept vs no-ept)?
# Answer 
When you compare the nested paging (with ept) with nested paging (no-ept), the number of exits for shadow paging keeps increasing.
