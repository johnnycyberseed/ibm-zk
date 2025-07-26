-
- Create and submit this JCL
- ```
  //W044ZD01 JOB(000000000,000000,00000000,00000000,0000).
  //         'W044ZD01 - MKVSAM',CLASS=A,MSGCLASS=X
  //         MSGLEVEL=(1,1)
  //DEFCLU   EXEC PGM=IDCAMS
  //SYSPRINT DD   SYSOUT=*
  //SYSIN    DD   *
    DEFINE CLUSTER(                  -
           NAME(W044Z.ADHOC.COMPTES) -
           KEYS(4 0)                 -
           RECORDS(50))
  /*
  ```
- Where
	- using the [[utility/IDCAMS]]'s ((6884eb00-63d1-4e59-bbba-309ee07ff2fb)) command
	-
	-