- Time Share Option
- An interactive shell for [[z/OS]]
- Includes a character-based GUI: [[ISPF]]
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
	- z/OS TSO/E Command Reference
		- https://www.ibm.com/docs/en/zos/2.5.0?topic=reference-tsoe-commands-subcommands
		-
	-