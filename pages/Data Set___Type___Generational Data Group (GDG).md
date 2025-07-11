- A collection of like-named [[Data Set/Type/Physical Sequential (PS)]]s
- New versions (or generations) are created over time
	- using the `(+1)` [[Data Set/Name (DSN)]] syntax
- Commonly used for managing
	- time-series data
	- backup data
- The [[Data Set/Name (DSN)]] is aka "GDG base name"
- One can create a GDG data set using the [[utility/IDCAMS]]
	- ```
	  //DEFGDG1   JOB  ...
	  //STEP1    EXEC PGM=IDCAMS
	  //SYSPRINT DD   SYSOUT=A
	  //SYSIN    DD   *
	       DEFINE GDG -
	             (NAME(userid.MYGDG.TEST) -
	             EMPTY -
	             NOSCRATCH -
	             LIMIT(15))
	  /*
	  ```
- Then, you can create a new generation using the [[utility/IEFBR14]]
-
-