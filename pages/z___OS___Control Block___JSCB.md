- Job-Step Control Block
- holds JCL- and JES-related data for a step and points to the chain of  [[z/OS/Control Block/TCB]]s / [[z/OS/Control Block/SRB]]s performing the work.
- Each job step running in the  [[address space]]  gets its own JSCB.
	- for example, one step in a batch job or a started task)
- the base for the job step environment, in particular [[SWA]] and [[z/OS/Control Block/Allocation]] Allocation.
-
-
- # References
	- https://www.ibm.com/docs/en/zos/2.5.0?topic=rqe-jscb-information