-
- # List Data Sets from TSO/E
	- ```
	    READY
	   LISTCAT ENTRIES(&DSN.)
	  ```
	-
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