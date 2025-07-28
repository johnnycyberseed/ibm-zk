- A list of common errors from [[JCL]] (and possible fixes)
-
- ## Missing DD statement
	- Observed:
		- Error in `JESYSMSG`
			- ```
			  UABORT CODE 36
			  AMSDUMP  DD STATEMENT MISSING
			  ```
	- Context
		- while using [[utility/IDCAMS]]
			- a [[JCL/DD]] for `SYSPRINT` was missing
	- Fix
		- add the `DD` statement for `SYSPRINT`
- ## Symbolic Name Mistyped (Quietly Failing)
	- Observed
	-
	-