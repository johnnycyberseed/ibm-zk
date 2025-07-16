-
- ## Components
  id:: 687680d9-563d-40d0-ad51-d8aec7833c3d
	- A part of a VSAM Data Set.
		- Each data set type has the appropriate components
			- [[Data Set/Type/VSAM/Key-Sequenced (KSDS)]] and [[Data Set/Type/VSAM/Variable-length Relative Record (VRRDS)]] include an ((6877d550-1374-4f20-9c13-05dab5bc7793))
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
		  collapsed:: true
			- collection of [[VSAM/Logical Record]]s
			- contains
				- the ((687664a2-e8a0-4c13-bc1e-64add9b7ff55))s
				- and the ((687664aa-f465-4c56-860c-eaf22bf31e25))s
				- of the logical records that contain those keys
			- these indexes are in a B-Tree like structure