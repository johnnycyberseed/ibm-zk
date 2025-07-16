- identified in one of three ways:
	- key field (the logical primary key)
	  id:: 687664a2-e8a0-4c13-bc1e-64add9b7ff55
		- can be up to 255 bytes in length
		- must be unique across the data set
		- There's also a secondary key or alternate key
			- does not need to be unique
			- see  [[VSAM/Alternate Index (AIX)]] for more.
	- Relative Byte Address (RBA)
	  id:: 687664aa-f465-4c56-860c-eaf22bf31e25
		- bytes from the beginning of the data set to the start of the record
		- can be translated into the ((6877f86b-4661-4ec6-a0a4-ed55341fdaf8))
	- Relative Record Number (RRN)
	  id:: 6877ea5c-4c5a-4654-8c55-ff8655832285
		- the index (zero-based) of the record; the 4th record has an RRN of 3.