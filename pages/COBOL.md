- **CO**mmon **B**usiness-**O**riented **L**anguage
- A COBOL program has the following structure:
	- [[COBOL/Division/Identification]]
	- [[COBOL/Division/Environment]]
	- [[COBOL/Division/Data]]
	- [[COBOL/Division/Procedure]]
- Each line of COBOL is broken into these areas:
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
- created
	- at IBM
	- by [[CODASYL]]
		- advised by Grace Hopper
	- to address the spiraling costs of creating and translating programs.
		- src: https://en.wikipedia.org/wiki/COBOL#Background
	-
- motivations
	- current programming languages are make/model-dependent.
	- data processing systems needed to adapt to rapidly change and expanding requirements
	- the current languages require significantly experienced staff to make those changes
- timeline
	- 1959
	- 1960 — COBOL-60
	- ...
	- 2023 — COBOL-2023
	- https://en.wikipedia.org/wiki/Timeline_of_programming_languages#1950s
- design influence
  id:: 686809b0-ff51-4220-be2c-4a1aa66705ab
	- [[FLOW-MATIC]]
		- "COBOL 60 was 95% [[FLOW-MATIC]]" — [[Grace Hopper]]
	- [[COMTRAN]]
	- [[AIMACO]]
- # References
	- https://en.wikipedia.org/wiki/COBOL
	- http://www.bitsavers.org/pdf/codasyl/COBOL_Report_Apr60.pdf
		- [[CODASYL]]'s initial specification
		-
	-