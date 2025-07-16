- There are two major parts of VSAM
	- Catalog Management
		- Q: how is this different than the z/OS "Catalog"?
		-
	- Record Management
		- see [[Data Set/Type/VSAM]] for Data Set types provided by VSAM
		-
		-
- # Key Concepts
	- ## Logical Record
	  id:: 687662db-b23c-4fdf-bd60-3fa4aa27010c
		- identified in one of three ways:
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
	- ## Physical Record
		- aka "Block"
	- ## Control Interval (CI)
	  id:: 687665f1-6fa5-473c-9ebe-c2c2ccffc353
		- can range from 512B to 32KB.
		- acts as a kind of window of access (fetching, mostly?)
	- ## Spanned Records
		- logical records that are larger than the ((687665f1-6fa5-473c-9ebe-c2c2ccffc353)).
	- ## Control Area (CA)
		-
	- ## Components
	  id:: 687680d9-563d-40d0-ad51-d8aec7833c3d
		- A part of a VSAM Data Set.
			- Each data set type has the appropriate components
				- [[Data Set/Type/VSAM/Key-Sequenced (KSDS)]] and [[Data Set/Type/VSAM/Virtual Relative Record (VRRDS)]] include an ((6877d550-1374-4f20-9c13-05dab5bc7793))
				- the sequential-ish data sets have ((6877d53a-f4ad-4b28-b644-b0e1b5cea803))s only
					- [[Data Set/Type/VSAM/Entry-Sequenced (ESDS)]]
					- [[Data Set/Type/VSAM/Relative Record (RRDS)]]
					- [[Data Set/Type/VSAM/Linear (LDS)]]
		- Each component has its own
			- name
			- entry in the [[Catalog]]
			- entry in the [[VTOC]]
		- there are two kinds of components:
			- ### data component
			  id:: 6877d53a-f4ad-4b28-b644-b0e1b5cea803
				-
			- ### index component
			  id:: 6877d550-1374-4f20-9c13-05dab5bc7793
				- collection of ((687662db-b23c-4fdf-bd60-3fa4aa27010c))s
				- contains
					- the ((687664a2-e8a0-4c13-bc1e-64add9b7ff55))s
					- and the ((687664aa-f465-4c56-860c-eaf22bf31e25))s
					- of the logical records that contain those keys
				- these indexes are in a B-Tree like structure
	- ## Clusters
	  id:: 6877d907-7742-4c3c-a2be-0102f222a207
		- one or two related ((687680d9-563d-40d0-ad51-d8aec7833c3d))
		- for each data set, there is an additional [[Catalog]] entry so that Data Sets with both ((6877d53a-f4ad-4b28-b644-b0e1b5cea803))s and ((6877d550-1374-4f20-9c13-05dab5bc7793))s can be referenced as a unit.
	- ## Alternate Indexes (AIX)
	  id:: 6877db4d-218c-4736-ad77-e66f253d84df
		- a [[Data Set/Type/VSAM/Key-Sequenced (KSDS)]] ((6877d907-7742-4c3c-a2be-0102f222a207))
		-
		-
		-
	- Sphere
- # Core Features of VSAM
	- https://chatgpt.com/share/e/687661a1-6f38-8001-a02a-ca93c2df5aa5
	- TL;DR. VSAM automates a lot of the nitty gritty
		- geometry of physical hardware (especially the 3390 disk drive)
		- writes "channel programs" in memory (called Virtual Channel Programs) which are micro-instructions for hardware while reading or writing.
		- supports an automatic WAIT on your task when you _must_ know when an I/O operation is completed.
-
-
- # References
	- https://www.ibm.com/docs/en/redbooks/vsam-demystified
		- PDF: https://www.redbooks.ibm.com/redbooks/pdfs/sg246105.pdf
	-