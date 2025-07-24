-
- # Add a PDS to the EXEC Library
	- e.g. with a PDS named `YOURID.REXX.EXEC` that contains a member named `IMSPING`
	- ```
	   READY
	  ALTLIB ACT APPL(EXEC) DA('YOURID.REXX.EXEC')
	   READY
	  IMSPING
	  ...
	  ```
	- and the REXX script `YOURID.REXX.EXEC(IMSPING)` gets executed.
-
-