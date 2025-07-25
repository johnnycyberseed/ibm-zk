- Time Share Option
- An interactive shell for [[z/OS]]
- Includes a character-based GUI: [[TSO/ISPF]]
- ## Logon
	- After logging on, TSO reports:
	- ```
	  (RACF msg) (username)  LAST ACCESS AT ...
	  (username) LOGON IN PROGRESS ...
	  (JES msg) (jobname) (username) STARTED  CPUA CN(00)
	  NO BROADCAST MESSAGES
	  
	  ```
		- for example:
		- `(RACF msg)` : `ICH70001I`
		- `(username)` : `TKMA6S1`
		- `(JES msg)` : `$HASP165`
		- `(jobname)` : `TSU34156`
-
- # References
	- z/OS TSO/E Command Reference, SA22-7782
		- https://publibz.boulder.ibm.com/epubs/pdf/ikj4c5b0.pdf
		-
	-