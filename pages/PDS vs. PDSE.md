- PDS (Partitioned Data Set) — the original
	- Has been around since the 1960s
	- Consists of a directory at the front and members stored sequentially after it
	- When you delete or replace a member, the old space is not reclaimed — it becomes "dead" space (called unused space or fragmentation)
	- Eventually the dataset fills up with dead space even if the actual data is small
	- You must periodically run IEBCOPY to compress it and reclaim that space — this is a maintenance burden and can't be done while the dataset is open
	- Directory size is fixed at allocation time — if you fill all your directory blocks, you can't add more members even if there's plenty of space for data
	- Max member size is limited to ~256MB (one extent worth of tracks)
- PDSE (Partitioned Data Set Extended) — the modern replacement
	- Introduced in the late 1980s/MVS/ESA era
	- Self-compressing: deleted/replaced member space is reclaimed automatically — no IEBCOPY needed
	- Directory is dynamic: grows as needed, never fills up independently of data space
	- Can be opened by multiple writers simultaneously (PDS allows only one writer at a time per member, but PDSE handles concurrent access more gracefully)
	- Supports larger members (up to ~3.2GB for PDSE V2 with z/OS 2.1+)
	- Cannot be used for load modules (executable programs) — load libraries must still be PDS. Use PDSE Program Object
	  libraries (DSNTYPE=LIBRARY,2) for that purpose on modern systems
- When you'd still use PDS
	- Load libraries (STEPLIB, LINKLST, etc.) — these must be PDS or a specific PDSE type
	- Very old shops with automation that assumes PDS behavior
	- Compatibility with old utilities that don't understand PDSE
- Rule of thumb
	- ▎ For source code, JCL, REXX, or any text-based library: always use PDSE (LIBRARY). Reserve PDS for load libraries or when
	  explicitly required.
	- One practical gotcha: some older ISPF utilities and certain TSO commands behave slightly differently with PDSE, but for
	  day-to-day editing and compiling COBOL, you'll never notice the difference — you just won't have to call your sysadmin to
	  compress your source library.