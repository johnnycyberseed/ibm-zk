- https://www.ibm.com/docs/en/cics-ts/5.6.0?topic=commands-inquire-task
-
- ```
  CEMT INQUIRE TASK
  ```
- Example output ([[BoaDia]])
	- ```
	     Tas(0000037) Tra(QRC3)           Run Tas Pri( 255 )
	        Sta(U ) Use(CICSTST ) Uow(E2964A01FD4B7401)
	     Tas(0000060) Tra(COPC)           Sus Tas Pri( 001 )
	        Sta(S ) Use(CICSTST ) Uow(E2964A02C81A4801) Hty(EKCWAIT )
	     Tas(0000065) Tra(OMEG)           Sus Tas Pri( 255 )
	        Sta(S ) Use(CICSTST ) Uow(E2964A04C017DF41) Hty(USERWAIT)
	     Tas(0000066) Tra(OMEG)           Sus Tas Pri( 255 )
	        Sta(S ) Use(CICSTST ) Uow(E2964A04C02FBF41) Hty(USERWAIT)
	     Tas(0004395) Tra(CEMT) Fac(A&FO) Run Ter Pri( 255 )
	        Sta(TO) Use(JOHNRYA ) Uow(E29D36328F5C0A80)
	  ```
- Where
	- `Sta` :: Start Code
		- `U` —
		- `TO` — Terminal Operator (via the CICS TS terminal screen, typing in the transaction ID... e.q. `CEMT`)
		- `S` — some other [[CICS/Task]] initiated this one — via a `START` command — with no data
		- `SD` — via a `START` command, _with_ data.
		-
		-