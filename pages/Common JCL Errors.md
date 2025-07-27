- A list of common errors from [[JCL]] (and possible fixes)
-
- ## Missing DD statement
	- ```
	  UABORT CODE 36
	  AMSDUMP  DD STATEMENT MISSING
	  ```
	- Observed
		- while using [[utility/IDCAMS]]
			- a [[JCL/DD]] for `SYSPRINT` was missing
			-
		-