- Multiple Virtual Storage
- The operating system introduced with the [[S/370]]
- Remains the foundational part of the operating system, today.
	- still a base component of [[z/OS]] providing
		- memory-management
		- core OS services
-
	-
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