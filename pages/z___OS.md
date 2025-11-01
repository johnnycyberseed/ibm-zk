- The most recent version of the operation system that runs on IBM mainframes
-
- Foundations
	- [[z/OS/Control Block]]
	- Storage
		- [[z/OS/CSTOR]]
		- [[z/OS/AUX]]
		- [[Virtual Storage]]
- Facilities
	- [[z/OS/RSM]]
	- [[SMS]]
-
- # Evolution
	- (diagram)
		- ```
		                      ┌────────────┐
		                      │  S/360 HW  │
		                      └────┬───────┘
		                           │
		         ┌─────────────────┴────────────────┐
		         │                                  │
		     ┌───▼───┐                         ┌─────▼─────┐
		     │ OS/360│                         │ DOS/360   │
		     └───┬───┘                         └────┬──────┘
		         │                                  │
		     ┌───▼───┐                         ┌────▼──────┐
		     │ MVT   │                         │ DOS/VS    │
		     └───┬───┘                         └────┬──────┘
		         │                                  │
		         │                                  │
		         └──────────────┬───────────────────┘
		                        │
		                  ┌─────▼─────┐
		                  │  MVS      │ (System/370)
		                  └────┬──────┘
		                       │
		                  ┌────▼──────┐
		                  │ MVS/XA    │ (Extended Arch)
		                  └────┬──────┘
		                       │
		                  ┌────▼──────┐
		                  │ MVS/ESA   │ (Enterprise SA)
		                  └────┬──────┘
		                       │
		                  ┌────▼──────┐
		                  │ OS/390    │
		                  └────┬──────┘
		                       │
		                  ┌────▼──────┐
		                  │  z/OS     │ (2001–Today)
		                  └───────────┘
		  ```
	-
- # References
	- z/OS Basics
		- Latest (Web): https://www.ibm.com/docs/en/zos-basic-skills
		- In Redbook format: https://www.redbooks.ibm.com/redbooks/pdfs/sg246366.pdf
	-
	- z/OS Documentation — https://www.ibm.com/docs/en/zos
	-
	-