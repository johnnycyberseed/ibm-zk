- Data Definition
-
- Common Params
	- `DISP`
		- ```
		  {DISP=[status]                                                        }
		  {DISP=([status][,normal-termination-disp][,abnormal-termination-disp])}
		  
		  DISP= ( [NEW] [,DELETE ] [,DELETE ] )
		          [OLD] [,KEEP   ] [,KEEP   ]
		          [SHR] [,PASS   ] [,CATLG  ]
		          [MOD] [,CATLG  ] [,UNCATLG]
		          [,  ] [,UNCATLG]
		                [,       ]
		  ```
		- `NEW` — data set is to be created in this step
		- `OLD` — the data set should exist; open in exclusive move
		-
- # References
	- https://www.ibm.com/docs/en/zos/3.1.0?topic=reference-dd-statement
	-