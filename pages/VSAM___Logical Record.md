- identified in one of three ways:
  collapsed:: true
	- key field (the logical primary key)
	  id:: 687664a2-e8a0-4c13-bc1e-64add9b7ff55
		- can be up to 255 bytes in length
		- must be unique across the data set
		- There's also a secondary key or alternate key
			- does not need to be unique
			- see ((6877db4d-218c-4736-ad77-e66f253d84df)) for more.
	- Relative Byte Address (RBA)
	  id:: 687664aa-f465-4c56-860c-eaf22bf31e25
		- bytes from the beginning of the data set to the start of the record
		- can be translated into the CCHHR value
			- CC = cylinder number
			- HH = track number
			- R = physical record number
	- Relative Record Number (RRN)
		- the index (zero-based) of the record; the 4th record has an RRN of 3.