- an kind of address space where application programs can run
	- aka "Processing Region"
- Application types
	- Transaction-oriented (aka "message-driven")
		- [[IMS/Dependent Region/MPR]]
		- [[IMS/Dependent Region/JMP]]
		- [[IMS/Dependent Region/IFP]]
		- [[IMS/Dependent Region/BMP]] (transaction-oriented)
		- Processing:
			- Gets a message from IMS
			  logseq.order-list-type:: number
			- Processes the message (typical doing DB access)
			  logseq.order-list-type:: number
			- Responds to the message
			  logseq.order-list-type:: number
	- Batch Processing (aka "Non-Message Processing")
		- [[IMS/Dependent Region/BMP]] (batch-oriented)
		- [[IMS/Dependent Region/JBP]]
		- for IMS systems with only IMS DB, this is the only kind of application that can be deployed
-
-