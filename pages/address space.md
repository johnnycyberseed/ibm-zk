- the runtime container where programs and their data are accessed
	- errors are isolated to the address space
- within an address space, users can start multiple tasks using [[z/OS/Control Block/TCB]]s
- analogous to a UNIX process
	- [[address space/ASID]]
- there are two methods of inter-address space communication
	- scheduling a [[z/OS/Control Block/SRB]] (asynchronously)
	- using cross-memory services and access registers (synchronously)
-
- ## Storage Map
  collapsed:: true
	- (diagram)
	  id:: 687fb224-d423-4332-9989-cef46c93324b
		- ![image.png](../assets/image_1753199094633_0.png)
- [[address space/private area]]
-
-
	-