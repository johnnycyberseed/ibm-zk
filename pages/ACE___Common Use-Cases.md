- A sample of practical uses of ACE ()
- # Transformations
	- ## Format/protocol conversion
	  collapsed:: true
		- JSON/REST → [[CICS/COMMAREA]]
			- the most fundamental transformation
			- converting a flexible JSON payload into the rigid fixed-length byte layout that the CICS COBOL program expects
				- matching exactly the field positions and lengths defined in the copybook
		- Response direction — converting the [[CICS/COMMAREA]] response back into JSON for the API consumer
		- COBOL error codes → HTTP semantics — mapping mainframe error codes/flags in the [[CICS/COMMAREA]] to meaningful HTTP status codes and error messages
	- ## Data type conversion
	  collapsed:: true
		- Date formats
			- ISO 8601 (2026-03-14) → COBOL date layout (20260314 or 140326 depending on the program)
		- Numeric types
			- JSON numbers → packed decimal (COMP-3) or zoned decimal as the COBOL copybook requires
		- Boolean → character flags
			- true/false → 'Y'/'N' or '1'/'0'
		- Currency/amounts — handling decimal precision money, ensuring correct implied decimal positioning in COBOL
	- ## Field formatting
	  collapsed:: true
		- Space-padding — COBOL fixed-length string fields must be padded to their exact defined length
		- Zero-padding — numeric fields often require leading zeros
		- Truncation handling — ensuring values don't overflow fixed-length fields
- # Enrichment
	- ## Identity and key translation
		- Customer ID mapping
		  collapsed:: true
			- translating a modern API customer identifier into the legacy customer number the mainframe has always known the customer by
			- these are frequently different
		- Product/SKU mapping
		  collapsed:: true
			- modern product IDs → legacy item codes in the mainframe's catalog
		- Store/branch code resolution
		  collapsed:: true
			- translating modern store identifiers to the branch codes the mainframe uses
	- ## Mainframe housekeeping fields
		- CICS programs written years ago often expect fields in the [[CICS/COMMAREA]] that have no equivalent in a modern API — ACE must inject these:
			- Operator ID / terminal ID — legacy fields that originated from 3270 terminal sessions
			- Date and time stamps — in the exact format the program expects
			- Transaction codes or function codes — internal flags the CICS program uses to determine what operation to perform
			- Region or branch context — which store/location is originating the request
	- Brazil-specific:
		- CPF/CNPJ formatting — Brazilian individual and corporate tax IDs have specific formats; ACE may validate and normalize these before passing to CICS
		- Tax code enrichment — Brazil has notoriously complex taxation (ICMS, ISS, PIS, COFINS); ACE may look up and inject applicable tax codes based on product, location, or transaction type
		- Correlation/audit ID injection — adding a transaction trace ID for end-to-end audit, which is important for Brazilian fiscal compliance requirements