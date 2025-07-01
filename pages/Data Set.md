- the mainframe equivalent of a file.
- identified by a [[Data Set/Name (DSN)]]
- kinds of [[Data Set]]s:
	- [[Data Set/Type/Sequential Data Set (PS)]]
	- [[Data Set/Type/Partitioned Data Set (PDS)]]
	- [[Data Set/Type/Extended PDS (PDSE)]]
	- [[Data Set/Type/Virtual Storage Access Method (VSAM)]]
	- [[Data Set/Type/Generational Data Group (GDG)]]
	- [[Data Set/Type/Hierarchical File System (HFS)]]
- {{renderer :mermaid_6863f97b-3bbe-432f-a9c4-018039b806ec, 4}}
	- ```mermaid
	  graph TD
	      A["Data Sets in z/OS"]
	  
	      %% Top-level categories
	      A --> B1["Sequential (PS)"]
	      A --> B2["Partitioned (PO)"]
	      A --> B3["Extended Partitioned (PDSE)"]
	      A --> B4["VSAM"]
	      A --> B5["Generation Data Group (GDG)"]
	      A --> B6["UNIX File Systems"]
	  
	      %% VSAM types
	      B4 --> C1["KSDS Key-Sequenced"]
	      B4 --> C2["ESDS Entry-Sequenced"]
	      B4 --> C3["RRDS Relative Record"]
	      B4 --> C4["LDS<br>Linear"]
	  
	      %% GDG versioning
	      B5 --> D1["Generation 0<br>(current)"]
	      B5 --> D2["Generation +1<br>(new)"]
	      B5 --> D3["Generation -1<br>(previous)"]
	  
	      %% Unix-style
	      B6 --> E1["HFS<br>(legacy)"]
	      B6 --> E2["zFS<br>(modern)"]
	  
	      %% Labels
	      classDef system fill:#f9f,stroke:#333,stroke-width:1px;
	      classDef vsam fill:#bbf,stroke:#333,stroke-width:1px;
	      class B4,C1,C2,C3,C4 vsam;
	      class B6,E1,E2 system;
	  ```