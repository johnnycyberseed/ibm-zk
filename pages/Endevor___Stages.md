- a stage in the software development lifecycle
- e.g. TEST, QA, FIX, PROD
- Stages have
	- a name
	- an ID (1 or 2)
- Stages are linked together to define promotion routes (i.e. "mapping")
	- [Endevor > Administrating > Defining Maps and Inventory Structures](https://techdocs.broadcom.com/us/en/ca-mainframe-software/devops/ca-endevor-software-change-manager/19-0/administrating/defining-maps-and-inventory-structures.html)
	- Sample mapping:
	- {{renderer :mermaid_68c2d2bb-ea11-4f9a-b4e7-fd46e2d6aeaa, 3}}
		- ```mermaid
		  graph LR
		    subgraph dev
		      UNIT
		      INT
		    end
		    subgraph QA_
		      QA
		      HOLD
		    end
		    subgraph PROD_
		      FIX
		      PROD
		    end
		    UNIT-->INT
		    INT-->QA
		    QA-->HOLD
		    HOLD-->PROD
		    FIX-->PROD
		  ```
-