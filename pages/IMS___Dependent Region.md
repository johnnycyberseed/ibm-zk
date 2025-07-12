- an address space where applications can run
- Application types
	- Transaction-oriented (aka "message-driven")
		- [[IMS/Dependent Region/MPR]]
		- [[IMS/Dependent Region/JMP]]
		- [[IMS/Dependent Region/IFP]]
		- Processing:
			- Gets a message from IMS
			  logseq.order-list-type:: number
			- Processes the message (typical doing DB access)
			  logseq.order-list-type:: number
			- Responds to the message
			  logseq.order-list-type:: number
	- Batch Processing (aka "Non-Message Processing")
		- [[IMS/Dependent Region/BMP]]
		- [[IMS/Dependent Region/JBP]]
		- for IMS systems with only IMS DB, this is the only kind of application that can be deployed
-