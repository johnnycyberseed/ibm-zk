- Process
	- Source is coded (e.g. in COBOL)
	  logseq.order-list-type:: number
		- typically in an [[FB80]] in a PDS (e.g. `&SYSUID.SRCELIB`)
		  logseq.order-list-type:: number
	- Source is compiled to an  [[object module]]
	  logseq.order-list-type:: number
		- typically in an [[FB80]] in a PDS (referred to as an [[object library]] )
		  logseq.order-list-type:: number
	- An [[object module]] is linked into a [[program module]]
	  logseq.order-list-type:: number
		- programmers can control the linking via
		  logseq.order-list-type:: number
	- logseq.order-list-type:: number
- Compilation, Linking, Loading, and Execution of [[program module]]s.
	- {{renderer :mermaid_69bf22d8-2912-463c-a385-5557f7731c59, 6}}
	  collapsed:: true
		- ```mermaid
		  flowchart TD
		      SM[("Source<p>modules")]
		      AC["Assembler<p>or compiler"]
		      OM[("Object<p>modules")]
		      PMB["Program<p>management<p>binder"]
		      LE["Linkage<p>editor"]
		      PO[("Program object<p>in<p>PDSE<p>program library<p>or z/OS UNIX file")]
		      LM[("Load module<p>in<p>PDS<p>program library")]
		      PML["Program<p>management<p>loader"]
		      BL["Batch<p>loader"]
		      PVS["Program<p>in virtual storage<p>ready for execution"]
		  
		      SM --> AC
		      AC --> OM
		      OM --> PMB
		      OM --> LE
		      PMB --> PO
		      PMB --> LM
		      LE --> LM
		      PO --> PML
		      LM --> PML
		      LM --> BL
		      BL --> PVS
		      PML --> PVS
		  ```
- # References
	- [[Program Management]]
	-
	- z/OS Basics: How programs are prepared to run: https://www.ibm.com/docs/en/zos-basic-skills?topic=zos-how-programs-are-prepared-run
		-
		-
	-