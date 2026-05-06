- Advanced Program-to-Program Communications
-
- As opposed to [[CICS/DTP/MRO]], which only supports CICS-to-CICS links on the same host
-
- Typical sequence between two processes:
	- [[CICS/Command/ALLOCATE]]
	  logseq.order-list-type:: number
		-
	- [[CICS/Command/CONNECT PROCESS]]
	  logseq.order-list-type:: number
	- [[CICS/Command/SEND]]
	  logseq.order-list-type:: number
	- [[CICS/Command/RECEIVE]]
	  logseq.order-list-type:: number
	- [[CICS/Commands/FREE]]
	  logseq.order-list-type:: number
-
- # References