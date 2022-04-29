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

#### Test
Start the nested VM and verify CPUID exit conditions using the test_assignment3.c file.
1. First run: result detail at : https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_3/first_run.txt
![image](https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_3/First_run.png)

2. Second run: result detail at : https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_3/second_run.txt
![image](https://github.com/Qinwang1993/CMPE-283/blob/master/Assignment_3/Second_run.png)

### 3. Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?
### Answer:
From the Result of first run and second run we can see that the number of exits is not increase at a stale rate. Operations like External Interrrupt, I/O instruction etc will cause more exits. About 1,500,000.
### 4. Of the exit types defined in the SDM, which are the most frequent? Least?
### Answer:
External Interrupt, cpuid, I/O instrcution, etc are the most frequent exit types. And MOV DR, INVD, etc are the least frequent exit types.


