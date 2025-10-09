- Character encoding.
- https://en.wikipedia.org/wiki/EBCDIC
-
- Acronym:
	- **E**xtended
	- **B**inary
	- **C**oded
	- **D**ecimal
	- **I**nterchage
	- **C**ode
-
- ## Convert to ASCII
	- ```
	  # for a EBCDIC file with 80 characters...
	  
	  dd if=input.file conv=ascii bs=80 | fold -w 80
	  ```
-