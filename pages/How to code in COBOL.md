-
- ## Periods
	- periods end a block.
	- Required:
		- Division / Section / Paragraph headers and Program-Level statements
			- ```COBOL
			          IDENTIFICATION DIVISION.
			          PROGRAM-ID. MYPROG.
			          WORKING-STORAGE SECTION.
			          FILE SECTION.
			          LINKAGE SECTION.
			          PROCEDURE DIVISION.
			          0001-MAIN.
			              STOP RUN.
			          0100-OPEN-FILES.
			  ```
	- Scoping:
		- Terminate scope of a statement
			- ```COBOL
			        * Legacy: scope terminated with periods
			          IF WS-EOF-FLAG = "Y"
			              DISPLAY 'End of File'.
			         
			        * Modern: explicit scope terminator
			          IF WS-EOF-FLAG = "Y"
			              DISPLAY 'End of File'
			          END-IF
			  ```
		- Simple Statements — not required but recommended
			- ```COBOL
			          DISPLAY 'Processing started'.
			          MOVE SPACES TO WS-WORK-AREA.
			          ADD 1 to WS-COUNTER.
			  ```
-