-
- # List details of specific data set (TSO)
	- To list a specific data set
	- ```
	    READY
	   LISTCAT ENTRIES(ADHOC.PROCLIB) ALL
	  ```
	- Note:
		- DSNs are automatically prefixed to your username
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
	- One of the many [[search path]]s in z/OS
- # Declare Data for a Program from the Command Line
	- Given a program that expects two files `DTTM` and `AUJDUI` (a compiled and linked COBOL program), you can wire these in analygous
	- ```
	  ALLOC DD(DTTM) DSN('W044Z.BAK.S001.X0227.DATE.CREATION')
	    READY
	  ALLOC DD(AUJDUI) DSN('W044.BAK.S001.X0227.DATES.SOUMIS')
	    READY
	  CALL 'W044Z.ADHOC.LOADLIB(SCRATCH)'
	   W4ZS0001 PROCESSING STARTED.
	   W4ZS0100 OPENING FILE(S).
	   W4ZS0101 DATE = 2025/09/16 16:54:14
	   W4ZS0199 CLOSING FILE(S).
	   W4ZS9999 PROCESSING COMPLETE.
	  ```
-