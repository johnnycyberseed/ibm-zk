- Virtual Telecommunications Access Manager
-
-
-
- Layering (diagram)
	- ```
	  +------------------------+
	  | Application Programs   |   <-- TSO, CICS, IMS, etc.
	  +------------------------+
	              |
	  +------------------------+
	  |      VTAM              |   <-- Session & communication management
	  +------------------------+
	              |
	  +------------------------+
	  |    SNA Network Stack   |   <-- LU (Logical Unit), PU (Physical Unit), etc.
	  +------------------------+
	              |
	  +------------------------+
	  |   Communications HW    |   <-- Channel-attached or remote network hardware
	  +------------------------+
	  ```