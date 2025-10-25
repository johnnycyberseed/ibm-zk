- the generic term for an executable on z/OS.
- there are two systems:
	- Legacy
		- (Source Listing) => Compiler => (object module) => Linkage Editor => (load module) => Batch Loader => (executable in memory)
			- load modules
				- legacy
				- limited to 16M in size
				- lives in a [[Data Set/Type/Partitioned Data Set (PDS)]]
	- Program Management (new)
		- (Source Listing) => Compiler => (object module) => Binder => (program object / load module) => Loader => (executable in memory)
			- program objects
				- newer
				- stored in a [[Data Set/Type/Extended PDS (PDSE)]]
-
- # How Program Modules are Made
	- Process
		- Source is coded (e.g. in COBOL)
		  logseq.order-list-type:: number
			- typically in an [[FB80]] in a PDS (e.g. `&SYSUID.SRCELIB`)
			  logseq.order-list-type:: number
		- Source is compiled to an  [[object module]]
		  logseq.order-list-type:: number
			- typically in an [[FB80]] in a PDS (referred to as an [[object library]] )
			  logseq.order-list-type:: number
		- An [[object module]] is linked into
		  logseq.order-list-type:: number
			- logseq.order-list-type:: number
		- logseq.order-list-type:: number
	- Diagram
		- ![image.png](../assets/image_1754180789322_0.png){:height 0, :width 800}
	-
-
- # References
	- Introduction to Program Mangement — https://www.ibm.com/docs/en/zos/2.5.0?topic=zmpmugr-introduction
	- z/OS Basics: How programs are prepared to run: https://www.ibm.com/docs/en/zos-basic-skills?topic=zos-how-programs-are-prepared-run
		-
		-
	-