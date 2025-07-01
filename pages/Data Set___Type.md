- kinds of [[Data Set]]s (rough order of sophistication):
	- [[Data Set/Type/Physical Sequential (PS)]] — like a flat file
	- [[Data Set/Type/Partitioned Data Set (PDS)]] — like a folder or archive
	- [[Data Set/Type/Extended PDS (PDSE)]] — new and improved PDS
	- [[Data Set/Type/VSAM]]
	- [[Data Set/Type/Generational Data Group (GDG)]]
	- [[Data Set/Type/Hierarchical File System (HFS)]] — Unix-like directory
	- Diagram...
	  collapsed:: true
		- {{renderer :mermaid_6863fa01-83ef-47a4-893a-ecac8b45712b, 5}}
		  collapsed:: true
			- ```mermaid
			  graph LR
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
			      B4 --> C4["LDS Linear"]
			  
			      %% GDG versioning
			      B5 --> D1["Generation 0 (current)"]
			      B5 --> D2["Generation +1 (new)"]
			      B5 --> D3["Generation -1 (previous)"]
			  
			      %% Unix-style
			      B6 --> E1["HFS (legacy)"]
			      B6 --> E2["zFS (modern)"]
			  
			      %% Labels
			      classDef system fill:#f9f,stroke:#333,stroke-width:1px;
			      classDef vsam fill:#bbf,stroke:#333,stroke-width:1px;
			      class B4,C1,C2,C3,C4 vsam;
			      class B6,E1,E2 system;
			  ```