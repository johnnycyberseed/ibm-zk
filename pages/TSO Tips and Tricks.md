-
- # List details of specific data set (TSO)
	- To list a specific data set
	- ```
	    READY
	   LISTCAT ENTRIES(ADHOC.PROCLIB) ALL
	  ```
	- Note:
		- DSNs are automatically prefixed to your
- # Add a PDS to the EXEC Library
	- e.g. with a PDS named `YOURID.REXX.EXEC` that contains a member named `IMSPING`
	- ```
	   READY
	  ALTLIB ACTIVATE APPLICATION(EXEC) DATASET('YOURID.REXX.EXEC')
	   READY
	  IMSPING
	  ...
	  ```
	- and the REXX script `YOURID.REXX.EXEC(IMSPING)` gets executed.
	- The above command can be abbreviated:
		- ```
		  ALTLIB ACT APP(EXEC) DA('YOURID.REXX.EXEC')
		  ```
	-