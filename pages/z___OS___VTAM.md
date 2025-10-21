- Virtual Telecommunications Access Manager
- Establishes and controls sessions
	- between users/devices (e.g., 3270 terminals/printers) and
	- host applications (e.g. TSO/ISPF, CICS, IMS), and
	- app-to-app via APPC/LU 6.2.
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