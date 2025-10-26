-
- ## Periods
	- periods end a block
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
	- Scoping
		- Terminate scope of a statement
			- ```COBOL
			  IF WS-EOF-FLAG = "Y"
			      DISPLAY 'End of File'
			  END-IF
			  ```