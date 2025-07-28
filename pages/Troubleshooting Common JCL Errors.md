- A list of common errors from [[JCL]] (and possible fixes)
-
- ## Missing DD statement
	- Context
		- while using [[utility/IDCAMS]] to perform a data set management operation
	- Observed
		- Error in `JESYSMSG`
			- ```
			  UABORT CODE 36
			  AMSDUMP  DD STATEMENT MISSING
			  ```
	- Fix
		- add the `DD` statement for `SYSPRINT`:
			- ```
			  ```
- ## Symbolic Name Mistyped (Quietly Failing)
	- Context
		- Using [[procedure/IGYWCLG]]
		- COBOL is deleting a record from a VSAM KSDS
			- ```cobol
			          FILE-CONTROL.
			              SELECT COMPTES-FILE ASSIGN TO 'COMPTES'
			  ```
		- Calling JCL names the DD:
			- ```jcl
			  //GO.COMPTE    DD DSN=W044Z.ADHOC.COMPTES,DISP=SHR
			  ```
	- Observed
		- Max-RC reported was 0 (no error reported)
		- In SDSF Status for Job, there was no output from the `GO` ProcStep
	-