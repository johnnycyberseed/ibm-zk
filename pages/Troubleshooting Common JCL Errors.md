- A list of common errors from [[JCL]] (and possible fixes)
-
- ## Missing DD statement
	- Observed
		- Error in `JESYSMSG`
			- ```
			  UABORT CODE 36
			  AMSDUMP  DD STATEMENT MISSING
			  ```
	- Context
		- while using [[utility/IDCAMS]] to perform a data set management operation
	- Fix
		- add the `DD` statement for `SYSPRINT`:
			- ```
			  ```
- ## Symbolic Name Mistyped (Quietly Failing)
	- Observed
		- Total Job reported
	-
	-