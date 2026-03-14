- Distributed Program Link
- basically, language-independent RPC in CICS
- the mechanism that allows one CICS program to call (or "link") to another
	- even in a remote CICS region
- How it works:
	- A program in one CICS region issues an EXEC CICS LINK command with a SYSID parameter specifying the target region
	  logseq.order-list-type:: number
	- CICS transparently ships the call to the remote region, executes the linked program there, and returns control (and data) back to the caller
	  logseq.order-list-type:: number
		- From the calling program's perspective, it looks nearly identical to a local LINK call
		-
- Key characteristics:
	- Synchronous — the calling program waits for the remote program to complete
	- Data passing via COMMAREA or channels/containers — same mechanisms as local LINK
	- The called program runs as a DPL mirror transaction (CSMI) in the target region
	- The called program cannot issue certain "conversational" commands — specifically it cannot do terminal I/O, which is why IBM documents a restricted command set for DPL target programs
	- The target program is sometimes called a DPL server program