- The 6th generation architecture of [[IBM]] mainframes
- The name was chosen to indicate the machines had zero downtime.
- Virtualization:
	- [[PR/SM]] (firmware layer)
		- [[LPAR]] A → runs z/OS directly
			- LPAR B → runs [[z/VM]]
				- VM1 → z/OS
				- VM2 → Linux
				- VM3 → [[z/VM]] (nested!)
- Offers six (6) Operating Systems
	- [[z/OS]]
	- [[z/VM]]
	- [[Linux]]
	- [[z/TPF]]
	- [[z/VSE]]
	- [[KVM]]
- Boasts the ability to house thousands of virtual machines
	- no extra network cables between systems
	- near-zero network delay between systems
	- no extra power supplies
- [[z/Storage Protection]]
-