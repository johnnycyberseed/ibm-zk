- the chain of control blocks owned by the MVS Allocation component that represent every data set or device assigned to this step
	- (e.g., TIOT, UCB, DEB structures).
- The [[z/OS/Control Block/JSCB]] anchors this chain so Allocation can locate, manage, and later free all resources when the step finishes.