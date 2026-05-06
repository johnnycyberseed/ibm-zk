- (built-in) Master Terminal Transaction
-
- ## Tips
	- ### Logging in to CICS TS
		- ```
		  CESN
		  ```
		- You are presented a form
			- In [[BomDia]]...
				- ```
				                              Signon to CICS                       APPLID CICSTST1
				  
				   DFHZC2312 ***  WELCOME TO CICS  ***
				  
				  
				  
				  
				   Type your userid and password, then press ENTER:
				  
				            Userid . . . .             Groupid . . .
				            Password . . .
				            Language . . .
				  
				        New Password . . .
				  
				  ```
		- On success you get the
			- `DFHCE3549 Sign-on is complete (Language ENU).`
		-
	- ### Command Help is `?` prefix
		- The following will show help for the command rather than execute it...
		- ```
		  ?CEMT INQUIRE TERMINAL
		  ```
- ## Common Commands
	- ### List registered [[CICS/Transaction]] s
		- [[CICS/INQUIRE TRANSACTION]]
	- ### List running [[CICS/Task]]s
		- [[CICS/INQUIRE TASK]]
		-
	- ###