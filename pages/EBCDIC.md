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
- Convert to
- ```
  # for a EBCDIC file with 80 characters...
  
  dd if=input.file bs=80 | fold -w 80
  ```