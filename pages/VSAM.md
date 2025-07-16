- There are two major parts of VSAM
	- Catalog Management
		- Q: how is this different than the z/OS "Catalog"?
		-
	- Record Management
		- see [[Data Set/Type/VSAM]] for Data Set types provided by VSAM
		-
- # Core Features
  collapsed:: true
	- https://chatgpt.com/share/e/687661a1-6f38-8001-a02a-ca93c2df5aa5
	- TL;DR. VSAM automates a lot of the nitty gritty
		- geometry of physical hardware (especially the 3390 disk drive)
		- writes "channel programs" in memory (called Virtual Channel Programs) which are micro-instructions for hardware while reading or writing.
		- supports an automatic WAIT on your task when you _must_ know when an I/O operation is completed.
- # Key Concepts
	- ## Logical Record
	  collapsed:: true
		- {{embed [[VSAM/Logical Record]]}}
	-
	- ## Physical Record
	  collapsed:: true
		- aka "Block"
		- VSAM data sets can only be defined on [[DASD]] devices.
		-
	- ## Control Interval (CI)
	  id:: 687665f1-6fa5-473c-9ebe-c2c2ccffc353
	  collapsed:: true
		- can range from 512B to 32KB.
		- acts as a kind of window of access (fetching, mostly?)
	- ## Spanned Records
	  collapsed:: true
		- logical records that are larger than the ((687665f1-6fa5-473c-9ebe-c2c2ccffc353)).
	- ## Control Area (CA)
	-
	- ## Component
		- {{embed [[VSAM/Component]]}}
		-
	- ## Cluster
	  id:: 6877d907-7742-4c3c-a2be-0102f222a207
		- one or two related [[VSAM/Component]]
		- for each data set, there is an additional [[Catalog]] entry so that Data Sets with both ((6877d53a-f4ad-4b28-b644-b0e1b5cea803))s and ((6877d550-1374-4f20-9c13-05dab5bc7793))s can be referenced as a unit.
	- ## Alternate Indexes (AIX)
	  id:: 6877db4d-218c-4736-ad77-e66f253d84df
		- a [[Data Set/Type/VSAM/Key-Sequenced (KSDS)]] ((6877d907-7742-4c3c-a2be-0102f222a207))
			- contains a ((6877d550-1374-4f20-9c13-05dab5bc7793)) and ((6877d53a-f4ad-4b28-b644-b0e1b5cea803))
			- allowing
				- logical records of a [[Data Set/Type/VSAM/Key-Sequenced (KSDS)]] or [[Data Set/Type/VSAM/Entry-Sequenced (ESDS)]] ((6877d907-7742-4c3c-a2be-0102f222a207))
			- to be accessed sequentially by more than one key field.
		- Can use the [[utility/IDCAMS]] to define and create an AIX.
			- by including the ((6877de3f-7502-4fe4-b15d-2373eaf086f6)) command
		- Before you can access such data sets via their alternate indexes, a path must be defined in the catalog
			- this is done through the [[utility/IDCAMS]]'s ((6877df4d-343a-4b81-b943-3600c5e8183f)) command
	-
		-
		-
		-
		-
	- ## Sphere
		- is
			- a base VSAM ((6877d907-7742-4c3c-a2be-0102f222a207)) and
			- all of its associated ((6877db4d-218c-4736-ad77-e66f253d84df))s.
		-
-
-
- # References
	- https://www.ibm.com/docs/en/redbooks/vsam-demystified
		- PDF: https://www.redbooks.ibm.com/redbooks/pdfs/sg246105.pdf
	-