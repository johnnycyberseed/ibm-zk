- A list of common errors from [[JCL]] (and possible fixes)
-
- ## Missing DD statement
	- ```
	  UABORT CODE 36
	  AMSDUMP  DD STATEMENT MISSING
	  ```
	- Observed
		- When a `SYSPRINT` was excluded