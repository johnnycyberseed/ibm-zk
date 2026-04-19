-
- # Troubleshooting Common Problems
	- ## Comments before `JOB` statement
		- **Symptom(s)**
			- When submitting the JCL, JES reports two jobs / job ids
		- **Diagnosis**
			- Line 1 _must_ be a `JOB` statement.
			- JES seeing Line 1 containing a comment as a missing `JOB` statement and attempts to prepend one.
		- **Prescription**
			- Move your `JOB` statement to line 1.
	- ## Missing leading space in `SET` statement
		- **Symptom(s)**
			- JES reports (in `JESYSMSG`) it's unable to parse the operation
				- ```
				           2 IEFC605I UNIDENTIFIED OPERATION FIELD
				  ```
			- The corresponding line in the JCL (in `JESJCL`) is a `SET` statement
				- ```JCL
				  //SET COBHLQ=IGY.V6R3M0
				  ```
		- **Diagnosis**
			- JES parsing JCL looks in column 3 to be the start of the "name" field.
			- It sees `SET` as that name and attempts to parse the remaining as an operator/statement
		- **Prescription**
			- Prefix the line with a leading space so that `SET` is interpreted as the operation
				- ```
				  // SET COBHLQ=IGY.V6R3M0
				  ```