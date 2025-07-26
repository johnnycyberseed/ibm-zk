-
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