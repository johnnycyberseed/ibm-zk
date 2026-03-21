- How to allocate a new [[Data Set/Type/Partitioned Data Set (PDS)]] from scratch.
-
- Note: if you're creating a PDS for your own purposes, consider creating a PDSE instead — [[PDS vs. PDSE]]
- # Step-by-Step
	- Data Set Utility
	  logseq.order-list-type:: number
		- `=3.2`
	- Enter DSN and `A` to Allocate
	  logseq.order-list-type:: number
	  collapsed:: true
		- ```
		     Menu  RefList  Utilities  Help
		   ──────────────────────────────────────────────────────────────────────────────
		                                  Data Set Utility
		  
		       A Allocate new data set                 C Catalog data set
		       R Rename entire data set                U Uncatalog data set
		       D Delete entire data set                S Short data set information
		   blank Data set information                  V VSAM Utilities
		  
		   ISPF Library:
		      Project  . .                  Enter "/" to select option
		      Group  . . .                  /  Confirm Data Set Delete
		      Type . . . .
		  
		   Other Partitioned, Sequential or VSAM Data Set:
		      Name  . . . . . . . MOCADE.LEARN.CICS.SRCLIB
		      Volume Serial . . .           (If not cataloged, required for option "C")
		  
		   Data Set Password  . .           (If password protected)
		  
		  
		   Option ===> A
		    F1=Help      F2=Split     F3=Exit      F7=Backward  F8=Forward   F9=Swap
		   F10=Actions  F12=Cancel
		  ```
	- Set (minimum) storage parameters
	  logseq.order-list-type:: number
- # Use-Cases
	- ## Source Code (small to medium)
		- Summary: the record format and length are dictated by the COBOL standard; the space values are a reasonable
		  starting estimate for development use; and LIBRARY is just the modern best practice.
		- Space units: **TRKS**
		  id:: 69bebcce-c608-4729-b3e2-f085d126b08e
			- Tracks are the classic unit for source libraries. They give you fine-grained control.
			- Cylinders (CYLS) are too coarse for small datasets (1 cylinder = 15 tracks on a 3390), and
			- KB/MB are convenient but obscure what's actually happening on disk.
			- Tracks let you size precisely without over-allocating.
		- Primary quantity: **10**
			- This is your initial allocation — grabbed at dataset creation time, and ideally contiguous on disk.
			- 10 tracks on a 3390 holds roughly 560 × 80-byte records (~45,000 lines of COBOL).
				- That's plenty for a learning/development library.
				- You'd go higher for a production source library shared by a team.
		- Secondary quantity: **5**
			- When the primary fills up, z/OS allocates an extent of this size.
			- You can get up to 16 extents (123 for PDSE), so secondary acts as a safety net rather than your main space.
			- Keeping it smaller than primary is intentional
				- if you're hitting secondary repeatedly, that's a signal to reallocate with a larger primary, not to rely on endless extensions.
		- Directory blocks: **20**
			- Each 256-byte directory block holds roughly 6–8 member entries. 20 blocks → ~120–160 members. For a learning library this is generous.
				- Note: for [[Data Set/Type/Extended PDS (PDSE)]] (LIBRARY type) this value is ignored — the directory grows dynamically — but ISPF still asks
				  for it and passes it along harmlessly.
		- Record format: **FB**
			- Fixed Blocked means every record is exactly the same length (Fixed), and multiple records are packed together into a block
			  (Blocked).
			- Variable-length formats would break compilers and editors expecting that
			  layout.
			- COBOL source requires fixed-length 80-byte records to conform to the standard column layout [[Format of a COBOL listing]]
		- Record length: **80**
			- The COBOL standard. [[Format of a COBOL listing]]
		- Block size: **0**
			- A block is how many bytes are physically written to disk in one I/O.
			- Using 0 tells z/OS to calculate the optimal blocksize itself
				- arguably better practice, since z/OS knows the geometry of the actual device.
			- 3120 is a good guess for smaller/medium files.
				- 3120 = 39 records × 80 bytes.
				- Fits efficiently into a 3390 track (which holds 56KB).
		- Data set name type: **LIBRARY**
			- Selects PDSE instead of traditional PDS.
			- As discussed, no compression needed, dynamic directory, concurrent access. The right default for any new source library.
	- ## Load Library
		- Space units: **TRKS**
			- same rational as source code libraries: {{embed ((69bebcce-c608-4729-b3e2-f085d126b08e))}}
		- Primary quantity: **30** (or more)
			- Compiled load modules are significantly larger than their source. Size depends on how many programs you expect.
		- Directory blocks: **50** (or more)
			- Load libraries tend to accumulate many members — one per compiled program.
				- Be more generous here than with source libraries since you can't easily expand a PDS directory later.
		- Record format: **U**
			- Load modules are variable-length binary objects — they don't fit in fixed 80-byte records.
			- Format U (Undefined) lets the system store records of any length, which is what the linkage editor writes.
		- Record length: **0**
			- With format U, record length is undefined — set it to 0.
		- Block size: **32760**
			- The maximum for format U. Larger block size = fewer I/Os = faster program fetch.
			- 32760 is the standard for load libraries.
		- Data set name type: **PDS**
			- load libraries must be [[Data Set/Type/Partitioned Data Set (PDS)]] , not PDSE/LIBRARY.
				- Traditional load modules cannot be stored in a PDSE.
		-
- # References
-