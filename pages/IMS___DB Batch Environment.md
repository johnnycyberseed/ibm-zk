- an ad-hoc batch region created to enable a batch program to perform IMS DB work
- aka "offline" IMS
- diagram
	- ![DB batch region has an application program and DL/I. DL/I reads from an update file and writes to a database. A TSO terminal submits jobs. The batch region writes to a log.](https://www.ibm.com/docs/en/SSEPH2_15.6.0/com.ibm.ims156.doc.sag/z0sag005.gif){:width 400}
- # DL/I Batch Processing
	- DL/I Call Flow Sequence Diagram
		- Procedures like [[DLIBATCH]] ultimately invoke [[DFSRRC00]]
		- Which prepare an environment for your "Application Program"
			- Which makes DL/I calls
			  collapsed:: true
				- e.g. for COBOL: https://www.ibm.com/docs/en/ims/15.4.0?topic=areas-coding-batch-program-in-cobol
			- Which is compiled and linked to the DFSLI000 via the IMS-supplied `IMSCOBOL` procedure
				- https://www.ibm.com/docs/en/ims/15.4.0?topic=cobol-binding-code-ims-language-interface-module
		- {{renderer :mermaid_68c427e4-70f7-42ad-a989-e19f05e289c5, 8}}
		  collapsed:: true
			- ```mermaid
			  sequenceDiagram
			      autonumber
			      participant JES as JES2/3
			      participant JCL as JCL Job (EXEC PGM=DFSRRC00)
			      participant RRC00 as DFSRRC00 (Batch DL/I driver)
			      participant APP as Application Program
			      participant LI as DFSLI000 (Language Interface)
			      participant DLI as DL/I Managers (in batch addr space)
			      participant IRLM as IRLM (optional)
			      participant VSAM as VSAM/OSAM Data Sets
			      participant LOG as IEFRDER / Batch Log
			  
			      JES->>JCL: Start job
			      JCL->>RRC00: PARM='DLI,prog,PSB,...'
			      RRC00->>APP: Load & initialize program
			      APP->>LI: DL/I call (e.g., GU/GN/ISRT/REPL/DLET)
			      LI->>DLI: Build PCB/DIB params, branch to DL/I
			  
			      alt Read call (e.g., GU/GN)
			          DLI->>VSAM: Locate & read CI/blocks
			          VSAM-->>DLI: Segment(s)
			          DLI-->>LI: Set PCB status + data
			          LI-->>APP: Return to caller
			      else Update call (ISRT/REPL/DLET)
			          opt DBRC/IRLM enabled
			              DLI->>IRLM: Lock request (db/dataset/record)
			              IRLM-->>DLI: Lock granted
			          end
			          DLI->>VSAM: Write/Update/CI split as needed
			          DLI->>LOG: Write log records (before/after images)
			          opt Checkpoint (CHKP)
			              APP->>LI: CHKP
			              LI->>DLI: Syncpoint/commit
			              DLI->>LOG: Checkpoint record
			              opt IRLM in use
			                  DLI->>IRLM: Release locks
			              end
			          end
			          VSAM-->>DLI: I/O complete
			          DLI-->>LI: Status (e.g., spaces/blank/' ' or GE/II/..)
			          LI-->>APP: Return to caller
			      end
			  
			      APP-->>RRC00: Program end
			      RRC00-->>JCL: Condition code & messages
			  ```
- # References and Resources
	- IMS Docs describing the DB Batch Environment
		- https://www.ibm.com/docs/en/ims/15.6.0?topic=configurations-db-batch-environment
	- IMS Docs describing the DBCTL Environment
		- https://www.ibm.com/docs/en/ims/15.6.0?topic=configurations-dbctl-environment#ims_dbctl_over
	- GPT5 regarding the runtime structures of DLIBATCH processing
		- https://chatgpt.com/share/e/68c42a17-8a64-8001-b14d-fb204ba34cc9
-
-