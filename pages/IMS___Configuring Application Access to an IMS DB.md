-
- Prior to version 14...
	- Metadata is configured via a set of control blocks
		- https://www.ibm.com/docs/en/ims/15.6.0?topic=design-using-ims-generation-utilities-ims-databases
	- IMS separates the concern of
		- Declare the structure of the database via [[IMS/DBD]]
		  logseq.order-list-type:: number
			- https://www.ibm.com/docs/en/ims/15.6.0?topic=databases-coding-database-descriptions-as-input-dbdgen-utility
			  logseq.order-list-type:: number
		- Define a program's usage of that DB with a [[IMS/PSB]]
		  logseq.order-list-type:: number
			- https://www.ibm.com/docs/en/ims/15.6.0?topic=uigudid-coding-program-specification-blocks-as-input-psbgen-utility
			  logseq.order-list-type:: number
			- More specifically, one or more [[IMS/PCB]]s
			  logseq.order-list-type:: number
		- [[IMS/ACB]]
		  logseq.order-list-type:: number
	- These configuration files are
		- coded using a set of Assembler macros
		- compiled and linked
		- stored in a [[Data Set/Type/Partitioned Data Set (PDS)]]
			- typically having a lowest-level qualifier of `DBDLIB` or `PSBLIB`, respectively.
- With the introduction of the [[IMS/Catalog]]...
	- DBDs are described using and heavily modified DDL SQL statements (with extensions)
		- https://www.ibm.com/docs/en/ims/15.6.0?topic=design-using-ddl-define-databases-program-views
	-