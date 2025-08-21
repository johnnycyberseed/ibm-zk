-
- Example
	- ```
	  //SMITH2   JOB 1,GEOFF,MSGCLASS=X
	  //         EXEC PGM=IEBGENER 
	  //SYSIN    DD DUMMY 
	  //SYSPRINT DD SYSOUT=X 
	  //SYSUT1   DD DISP=SHR,DSN=SMITH.SEQ.DATA 
	  //SYSUT2   DD DISP=(NEW,CATLG),DSN=SMITH.COPY.DATA,UNIT=3390, 
	  //   VOL=SER=WORK02,SPACE=(TRK,3,3)) 
	  ```
	- `SYSIN` — the control card
	-
- # References
	- https://www.ibm.com/docs/en/zos-basic-skills?topic=utilities-iebgener-utility-generate-copy-sequential-data-set
	-