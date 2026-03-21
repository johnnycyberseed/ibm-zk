- Each line of COBOL is broken into five areas:
	- ```
	           11111111112222222222333333333344444444445555555555666666666677777777778
	  12345678901234567890123456789012345678901234567890123456789012345678901234567890
	  |    |^|  ||                                                           ||      |
	  |    |:|  ||                                                           ||      |
	  Seq   : \ | \_________________________________________________________/  \____/
	  Num   :  \|                       B Area (12-72)                          Identification
	  Area  :   A Area (8-11)                                                   Area (73-80)
	  (1-6) :
	        Indicator
	        Area
	        (7)
	  ```
	- That is:
		- Sequence Number Area (1-6) —
		- Indicator Area (7)
			- `*` = line is a comment
			- `D` = line is a debug statement
			- `-` = line continuation
			- `/` = source formatter
		- A Area (8-11) — structure definition divisions, sections, level indicators
		- B Area (12-72) — statements, sentences, and clauses
		- Identification Area (73-80) — ignored by the compiler (can use for comments)
	-