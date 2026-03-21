- https://chatgpt.com/share/e/69bd7ce6-3234-8001-9006-b41e7fb95890
- # Overview
  collapsed:: true
	- This tutorial gives you two practical, end-to-end “from nothing to running” paths for a first CICS program on z/OS:
	- ## Absolute Minimum Path
		- The minimal path proves your toolchain and CICS install process with a single COBOL program that issues `EXEC CICS SEND TEXT` (no BMS screen).
		- You will:
			- create source + JCL → translate `EXEC CICS`
			  logseq.order-list-type:: number
			- compile with Enterprise COBOL
			  logseq.order-list-type:: number
			- link-edit (binder) including the required CICS HLL interface stub `DFHELII`
			  logseq.order-list-type:: number
			- place the load module into a library CICS can load from (static `DFHRPL` or a dynamic `LIBRARY`)
			  logseq.order-list-type:: number
			- define a CICS `PROGRAM` and `TRANSACTION` in RDO (`CEDA`)
			  logseq.order-list-type:: number
			- `CEDA INSTALL`
			  logseq.order-list-type:: number
			- run the transaction from a 3270 terminal.
			  logseq.order-list-type:: number
		- IBM describes this translate/compile/link process (and the need to include the proper EXEC interface module) as the standard preparation model for command-level CICS programs.
		- Jump to this path: ((69bec8f6-bb9f-4e48-a722-70367d175aaa))
	- ## Optional BMS path
		- The optional BMS path adds a single BMS mapset and a simple pseudo-conversational screen flow using `SEND MAP` and `RECEIVE MAP`.
		- You will:
			- create a BMS map (DFHMSD/DFHMDI/DFHMDF)
			- run `DFHMAPS` to generate both the physical map load module and the COBOL symbolic map copybook
			- compile/link the COBOL program that `COPY`s the symbolic map
			- define/install the `MAPSET` and related `PROGRAM` and `TRANSACTION`
			- run and iterate using `CEMT SET PROGRAM(... ) NEWCOPY`.
		- IBM’s BMS docs explicitly distinguish physical vs symbolic map sets and show `DFHMAPS` as the combined build procedure.
		- Start with this path: ((69bec8f6-bb9f-4e48-a722-70367d175aaa))
		- Folding in this path: ((69bec8f6-22ff-47be-9a79-24a77c12f8db))
- # Assumptions and prerequisites
  collapsed:: true
	- ## Software Installed
	  collapsed:: true
		- a working z/OS environment
		- with IBM CICS Transaction Server for z/OS (CICS TS) installed,
		- you can log on to a CICS region from a 3270 terminal emulator.
	- ## Permissions
	  collapsed:: true
		- can submit batch JCL (e.g., via ISPF/SDSF)
		- you have access to
			- an Enterprise COBOL compiler (`IGYCRCTL`)
			- the Language Environment binder libraries needed for link-edit.
		- have read access to the CICS product libraries (commonly `&CICSHLQ..SDFHLOAD`, `SDFHCOB`, `SDFHMAC`, `SDFHPROC`)
		- have authority to
			- define/install resources with `CEDA` and
				- `CEDA` defines resources in the CSD and can also update the running system;
				- there is no resource/command security checking inside CEDA itself
			- manage programs with `CEMT` (or you can ask a CICS admin to perform those steps for you).
		- Note: IBM’s CICS sample “install COBOL application programs” and “using your own job streams” material assumes this toolchain model.
	- ## Configuration
	  collapsed:: true
		- can load application modules from either `DFHRPL` (static) or a dynamic `LIBRARY` resource.
			- DFHRPL is defined in startup JCL and cannot be changed without restart,
				- motivating dynamic `LIBRARY` usage.
	- ## Translator choice: separate vs integrated
	  collapsed:: true
		- This tutorial shows a **separate translator step** first because it makes the pipeline explicit:
			- translate → compile → link-edit.
		- IBM lists the CICS stand-alone COBOL translator as `DFHECP1$`,
		- and also warns the separate translator is not updated for newer COBOL language features (recommending the integrated translator for newest COBOL features).
		- If your shop uses the integrated translator (Enterprise COBOL `CICS(...)` compiler option),
		- you can still follow the **same deployment steps**, but your JCL changes.
		- IBM provides sample JCL for both separate and integrated translator pipelines.
- # Artifact inventory and dataset conventions
  collapsed:: true
	- ## Files you will create
	  collapsed:: true
		- The table uses the placeholders you requested: `&HLQ`, `&CICSHLQ`, `&SRC`, `&COPY`, `&LOAD`. In the JCL templates, these are set via `//SET` (symbolic parameters) so you can quickly adapt them.
		- | Artifact (member) | Type | Purpose | Suggested dataset/member convention |
		  |---|---|---|---|
		  | `HELLOTXT` | COBOL source | Minimal CICS program using `EXEC CICS SEND TEXT` | `&SRC(HELLOTXT)` |
		  | `BMSHELLO` | COBOL source | Optional screen program using `SEND MAP` / `RECEIVE MAP` | `&SRC(BMSHELLO)` |
		  | `HWMAP1` | BMS map source (HLASM macros) | Mapset + map + fields (built by DFHMAPS) | `&SRC(HWMAP1)` |
		  | `COMPCICS` | JCL | Translate + compile + link-edit a CICS COBOL program (explicit steps) | `&HLQ..CICSDEMO.JCL(COMPCICS)` |
		  | `CALLPROC` | JCL | Optional: call IBM-supplied PROC (if enabled at your site) | `&HLQ..CICSDEMO.JCL(CALLPROC)` |
		  | `ASMBMS` | JCL | Build BMS physical+symbolic maps via `DFHMAPS` | `&HLQ..CICSDEMO.JCL(ASMBMS)` |
		  | `HWMAP1` | COPYBOOK (generated) | Symbolic map copybook emitted by DFHMAPS (`SYSPUNCH`) | `&COPY(HWMAP1)` |
		  | `HELLOTXT`, `BMSHELLO`, `HWMAP1` | Load modules | Executable program(s) and physical mapset for CICS to load | `&LOAD(HELLOTXT)` etc. |
	- ## Workflow Overview
		- Preparation of command-level CICS programs as:
		- translator converts `EXEC CICS` into language-level calls;
		- you then compile and link-edit, including the required EXEC interface module.
		- {{renderer :mermaid_69beca6b-611e-44f2-a60d-8c582ebcd06d, 6}}
			- ```mermaid
			  flowchart TD
			    A["Write COBOL source<p>EXEC CICS ... END-EXEC"] --> B["Translate DFHECP1$<p>(stand-alone)<p>or integrated translator"]
			    B --> C["Compile IGYCRCTL<p>(Enterprise COBOL)"]
			    C --> D["Link-edit (binder)<p>INCLUDE DFHELII<p>Output to &LOAD"]
			    A -->|Optional BMS| E["Write BMS map macros<p>DFHMSD/DFHMDI/DFHMDF"]
			    E --> F["DFHMAPS proc<p>creates physical+symbolic maps"]
			    F --> G["Physical mapset load module -> &LOAD"]
			    F --> H["Symbolic map copybook -> &COPY"]
			    D --> I["Make &LOAD visible to CICS<p>DFHRPL or dynamic LIBRARY"]
			    G --> I
			    I --> J["Define resources (RDO)<p>CEDA DEFINE PROGRAM/TRANSACTION<p>+ MAPSET if BMS"]
			    J --> K["Install into running region<p>CEDA INSTALL"]
			    K --> L["Run transaction from 3270"]
			    D --> M["Iterate changes<p>CEMT SET PROGRAM(...) NEWCOPY"]
			    G --> M
			  ```
- # Minimal path: SEND TEXT with no BMS
  id:: 69bec8f6-bb9f-4e48-a722-70367d175aaa
  collapsed:: true
	- This path is the fastest “first win” because it avoids BMS maps entirely and relies on `SEND TEXT`,
		- which IBM describes as sending text data “without mapping.”
	- ### Step-by-step actions a developer executes
	- #### Setup steps
	  
	  1) **Pick your placeholder values** for the JCL variables:
		- `&HLQ` (your user high-level qualifier)
		- `&CICSHLQ` (your site’s CICS TS product HLQ that owns `SDFHLOAD`, `SDFHCOB`, `SDFHMAC`, `SDFHPROC`)
		- `&SRC` (your source library dataset name)
		- `&COPY` (your copybook library)
		- `&LOAD` (your load library that CICS will search via DFHRPL or LIBRARY)
		  
		  IBM’s examples assume shipped libraries like `CICSTSnn.CICS.SDFHLOAD` / `SDFHPROC` exist, where `nn` is the release. citeturn9view2turn6search0  
		  (confidence: 0.75)
		  
		  2) **Allocate datasets** (PDSE recommended for load libraries; PDS/PDSE for source/copy/JCL). This is site-standard (IDCAMS, ISPF 3.2, or your shop tooling). Ensure the load library is a proper program library type your CICS region can load from.  
		  (confidence: 0.6)  
		  Assumptions:
		- Your shop allows you to allocate `&SRC`, `&COPY`, and `&LOAD`.
		- Your CICS region can access the resulting datasets (RACF/ACF2/TSS rules vary).
		  
		  3) **Confirm how your CICS region will find load modules**:
		- **DFHRPL path**: ask a sysprog which datasets are in DFHRPL for the region, or locate the region startup JCL and look for the `DFHRPL` DD concatenation. IBM explains DFHRPL is defined at startup and is not changeable without restarting CICS. citeturn1search2turn7search10
		- **Dynamic LIBRARY path**: confirm whether your region uses dynamic program library resources (`LIBRARY`) and whether you are allowed to define/install them. IBM documents the LIBRARY resource model and that DFHRPL is a “special” LIBRARY that cannot be altered in a running region. citeturn7search14turn1search2  
		  (confidence: 0.72)
	- #### Create and build the minimal program
	  
	  4) **Create COBOL program source** member `&SRC(HELLOTXT)` exactly as follows.
	  
	  ```cobol
	       IDENTIFICATION DIVISION.
	       PROGRAM-ID. HELLOTXT.
	  
	       DATA DIVISION.
	       WORKING-STORAGE SECTION.
	       01  WS-MSG   PIC X(80)
	           VALUE 'HELLO FROM CICS: SEND TEXT (no BMS).'.
	  
	       01  WS-RESP  PIC S9(9) COMP VALUE 0.
	       01  WS-RESP2 PIC S9(9) COMP VALUE 0.
	  
	       PROCEDURE DIVISION.
	       MAIN.
	           EXEC CICS
	                SEND TEXT
	                FROM(WS-MSG)
	                LENGTH(LENGTH OF WS-MSG)
	                ERASE
	                FREEKB
	                RESP(WS-RESP)
	                RESP2(WS-RESP2)
	           END-EXEC
	  
	           EXEC CICS
	                RETURN
	           END-EXEC.
	  
	           GOBACK.
	  ```
	  
	  IBM’s `SEND TEXT` command reference documents that it sends text data without mapping. citeturn3search0turn3search8  
	  IBM’s `RESP`/`RESP2` documentation explains that `RESP` returns a value (normally `DFHRESP(NORMAL)`) corresponding to the condition that might have been raised. citeturn4search1turn4search10  
	  (confidence: 0.86)
	  
	  5) **Create the translate/compile/link-edit JCL** member (example name `&HLQ..CICSDEMO.JCL(COMPCICS)`) using explicit steps and your requested placeholders.
	  
	  Important IBM requirement: for online programs using `EXEC CICS`, the link-edit input must include the correct interface module before the object deck, and for HLL languages that module is `DFHELII`. IBM shows that omitting it leads to unresolved externals and “not executable.” citeturn9view2turn0search0turn6search1
	  
	  ```jcl
	  //* --------------------------------------------------------------
	  //* COMPCICS: Explicit translate + compile + link-edit (binder)
	  //* Change only the SET symbols and the MEMBER/PGMNAME values.
	  //* --------------------------------------------------------------
	  //COMPCICS JOB (ACCT),'CICS COBOL',CLASS=A,MSGCLASS=X,NOTIFY=&SYSUID
	  //SET HLQ=YOUR.HLQ
	  //SET CICSHLQ=CICSTSXX.CICS
	  //SET SRC=&HLQ..CICSDEMO.SRC
	  //SET COPY=&HLQ..CICSDEMO.COPY
	  //SET LOAD=&HLQ..CICSDEMO.LOAD
	  //SET MEMBER=HELLOTXT
	  //SET PGMNAME=HELLOTXT
	  
	  //* --- STEP 1: Translate EXEC CICS using stand-alone translator
	  //* IBM identifies the COBOL separate translator as DFHECP1$. 
	  //TRN     EXEC PGM=DFHECP1$,REGION=4M,
	  //         PARM='COBOL3,APOST,CICS'
	  //STEPLIB  DD  DSN=&CICSHLQ..SDFHLOAD,DISP=SHR
	  //SYSPRINT DD  SYSOUT=*
	  //SYSPUNCH DD  DSN=&&TRNOUT,DISP=(,PASS),UNIT=SYSDA,
	  //             SPACE=(TRK,(10,10)),DCB=(RECFM=FB,LRECL=80,BLKSIZE=0)
	  //SYSIN    DD  DSN=&SRC(&MEMBER),DISP=SHR
	  
	  //* --- STEP 2: Compile translated output with Enterprise COBOL
	  //* IBM sample guidance: RENT and NODYNAM are required for COBOL programs.
	  //COB     EXEC PGM=IGYCRCTL,REGION=0M,
	  //         PARM='OBJECT,RENT,NODYNAM,APOST,MAP,XREF'
	  //STEPLIB  DD  DSN=YOUR.COBOL.COMPILER.SIGYCOMP,DISP=SHR
	  //SYSLIB   DD  DSN=&COPY,DISP=SHR
	  //         DD  DSN=&CICSHLQ..SDFHCOB,DISP=SHR
	  //         DD  DSN=&CICSHLQ..SDFHMAC,DISP=SHR
	  //SYSPRINT DD  SYSOUT=*
	  //SYSIN    DD  DSN=&&TRNOUT,DISP=(OLD,DELETE)
	  //SYSLIN   DD  DSN=&&OBJ,DISP=(,PASS),UNIT=SYSDA,
	  //             SPACE=(TRK,(10,10))
	  
	  //* --- STEP 3: Link-edit (binder) and write load module
	  //* Must include DFHELII for HLL programs.
	  //LKED    EXEC PGM=IEWL,REGION=0M,COND=(5,LT,COB),
	  //         PARM='LIST,XREF,AMODE=31,RMODE=ANY'
	  //SYSLIB   DD  DSN=&CICSHLQ..SDFHLOAD,DISP=SHR
	  //         DD  DSN=YOUR.LE.SCEELKED,DISP=SHR
	  //SYSPRINT DD  SYSOUT=*
	  //SYSLMOD  DD  DSN=&LOAD(&PGMNAME),DISP=SHR
	  //SYSLIN   DD  *
	  INCLUDE SYSLIB(DFHELII)
	  NAME &PGMNAME(R)
	  /*
	  //         DD  DSN=&&OBJ,DISP=(OLD,DELETE)
	  ```
	  
	  Why these specific elements:
	- `DFHECP1$` is IBM’s COBOL stand-alone CICS translator. citeturn11search13turn11search5
	- IBM’s sample JCL for COBOL application programs states you need compiler options **RENT** and **NODYNAM**. citeturn9view1
	- IBM requires `DFHELII` to be included for HLL programs at link-edit. citeturn9view2turn0search4turn6search1  
	  (confidence: 0.74)  
	  Assumptions:
	- Your site’s COBOL compiler load library (`SIGYCOMP`) and LE binder library (`SCEELKED`) dataset names differ from the placeholders.
	- Your standards might require additional dependencies (DB2, IMS, MQ). This tutorial assumes none.
	  
	  6) **Submit the JCL** and verify:
		- Translator step `TRN` return code = 0 (or acceptable per your standards).
		- Compile step `COB` return code is acceptable.
		- Link-edit step produces member `&LOAD(HELLOTXT)`.
		  
		  IBM’s “Using your own job streams” explicitly ties success to correct interface module inclusion at link-edit. citeturn9view2  
		  (confidence: 0.8)
	- #### Make the program loadable by the CICS region
	  
	  7) **Choose one** of the two ways to make `&LOAD` visible to the region (do not skip).
	  
	  **Option A — DFHRPL (static)**  
	  8A) Ask your sysprog/admin to add `&LOAD` to the region startup JCL `DFHRPL` concatenation (requires restart). IBM notes DFHRPL changes are not possible while CICS is running. citeturn1search2turn7search10  
	  (confidence: 0.6)  
	  Assumptions:
	- You cannot edit production region JCL; you may need a dev/test region.
	  
	  **Option B — dynamic LIBRARY (preferred in many test setups)**  
	  8B) Define a `LIBRARY` resource (example name `HWDLOAD`) that points to `&LOAD`.
	  
	  IBM documents LIBRARY resource definitions as representing PDS/PDSE concatenations used for program artifacts and that DFHRPL is a special static case. citeturn7search14turn7search3  
	  (confidence: 0.75)
	  
	  Concrete actions (dynamic LIBRARY):
	  9B) In CICS, run:
	  
	  ```text
	  CEDA DEFINE LIBRARY(HWDLOAD) GROUP(HWDEMO)
	  ```
	  
	  10B) On the LIBRARY definition panel, set:
	- `DSNAME01` = `&LOAD` (your actual dataset name, e.g., `USER01.CICSDEMO.LOAD`)
	- `CRITICAL` = `NO` (typical for dev/test; choose per your site policy)
	  
	  IBM’s LIBRARY attribute reference documents DSNAME01–16 as the dataset names for the concatenation. citeturn7search3turn7search14  
	  (confidence: 0.7)
	  
	  11B) Install and enable:
	  
	  ```text
	  CEDA INSTALL LIBRARY(HWDLOAD) GROUP(HWDEMO) STATUS(ENABLED)
	  ```
	  
	  IBM provides this exact “install LIBRARY by using CEDA” pattern. citeturn7search2  
	  (confidence: 0.8)
	  
	  12B) Verify CICS sees it:
	  
	  ```text
	  CEMT INQUIRE LIBRARY(HWDLOAD)
	  ```
	  
	  IBM documents `CEMT INQUIRE LIBRARY`. citeturn7search1  
	  (confidence: 0.78)
	- #### Define the CICS resources and run
	  
	  13) **Define a PROGRAM resource** for your load module:
	  
	  ```text
	  CEDA DEFINE PROGRAM(HELLOTXT) GROUP(HWDEMO)
	  ```
	  
	  IBM documents that PROGRAM resources control information used to process a transaction, and that they can be created via CEDA. citeturn2search7turn2search3  
	  (confidence: 0.75)
	  
	  14) On the PROGRAM panel, set or confirm common defaults:
	- `LANGUAGE` = `COBOL`
	- `STATUS` = `ENABLED` (or enable later)
	  
	  (The exact panel fields vary by CICS TS release/site standards; the resource exists either way.) citeturn2search0  
	  (confidence: 0.65)  
	  Assumptions:
	- Your site uses RDO panels rather than bundles or DFHCSDUP pipelines.
	  
	  15) **Define a TRANSACTION** that points to the program (choose a 4-character ID not reserved by your shop):
	  
	  ```text
	  CEDA DEFINE TRANSACTION(HTX1) GROUP(HWDEMO)
	  ```
	  
	  On the TRANSACTION panel:
	- `PROGRAM` = `HELLOTXT`
	  
	  IBM notes that at a minimum you must define a transaction before you can run a program in CICS, and it defines TRANSACTION resources as defining transaction attributes and providing the TRANSID. citeturn2search21turn2search1  
	  (confidence: 0.8)
	  
	  16) **Install the group into the running region**:
	  
	  ```text
	  CEDA INSTALL GROUP(HWDEMO)
	  ```
	  
	  IBM’s `CEDA INSTALL` reference states it makes the resource definitions in the named group available to the active CICS system. citeturn0search3turn2search19  
	  (confidence: 0.9)
	  
	  17) **Run the transaction** from your 3270 terminal: type `HTX1` and press Enter.
	  
	  Mock 3270 screenshot (mockup — include inline in your notes/wiki near this step):
	  
	  ```text
	  +------------------------------------------------------------------------------+
	  | CICS REGION: DEV1                         DATE: 2026-03-13                   |
	  |                                                                              |
	  | ==> HTX1                                                                     |
	  |                                                                              |
	  |                                                                              |
	  |                                                                              |
	  |                                                                              |
	  +------------------------------------------------------------------------------+
	  ```
	  
	  18) You should see a blanked screen with your message.
	  
	  Mock 3270 screenshot (mockup):
	  
	  ```text
	  +------------------------------------------------------------------------------+
	  | HELLO FROM CICS: SEND TEXT (no BMS).                                         |
	  |                                                                              |
	  |                                                                              |
	  |                                                                              |
	  |                                                                              |
	  |                                                                              |
	  |                                                                              |
	  |                                                                              |
	  +------------------------------------------------------------------------------+
	  ```
	  
	  IBM’s `SEND TEXT` is explicitly “without mapping.” citeturn3search0  
	  (confidence: 0.85)
	  
	  19) **Iterate**: after you recompile/link a new version into the same `&LOAD(HELLOTXT)` member, issue:
	  
	  ```text
	  CEMT SET PROGRAM(HELLOTXT) NEWCOPY
	  ```
	  
	  IBM’s `CEMT SET PROGRAM` documentation explains NEWCOPY/PHASEIN behavior (new copy used for new requests while old runs finish) and that CICS loads the new version from DFHRPL or dynamic LIBRARY concatenation. citeturn1search0turn7search15  
	  (confidence: 0.85)
- # Optional path: add a BMS map and use SEND MAP / RECEIVE MAP
  id:: 69bec8f6-22ff-47be-9a79-24a77c12f8db
  collapsed:: true
	- Continue here after the minimal path works. IBM’s BMS documentation emphasizes physical vs symbolic map sets and that physical map sets must be loadable by CICS and require a MAPSET resource definition.
	- ### Step-by-step actions
	- 20) **Create BMS map source** member `&SRC(HWMAP1)` using DFHMSD/DFHMDI/DFHMDF macros.
	  
	  IBM’s BMS macro summary documents the roles: DFHMSD defines a mapset, DFHMDI defines a map, DFHMDF defines a field. citeturn5search21turn5search2
	  
	  ```asm
	         PRINT NOGEN
	  HWMAP1   DFHMSD TYPE=&SYSPARM,MODE=INOUT,LANG=COBOL,STORAGE=AUTO,      X
	               TIOAPFX=YES,CTRL=(FREEKB,FRSET),TERM=3270
	  
	  HWMAP    DFHMDI SIZE=(24,80),LINE=1,COLUMN=1,CTRL=(FREEKB,FRSET)
	  
	  TITLE    DFHMDF POS=(1,2),LENGTH=30,ATTRB=(PROT,BRT),                 X
	               INITIAL='CICS BMS HELLO'
	  
	  PROMPT   DFHMDF POS=(4,2),LENGTH=11,ATTRB=(PROT,NORM),                X
	               INITIAL='Name: '
	  
	  NAME     DFHMDF POS=(4,13),LENGTH=20,ATTRB=(UNPROT,IC,FSET),          X
	               INITIAL=' '
	  
	  MSGLBL   DFHMDF POS=(6,2),LENGTH=10,ATTRB=(PROT,NORM),                X
	               INITIAL='Message:'
	  
	  MSG      DFHMDF POS=(6,13),LENGTH=60,ATTRB=(PROT,BRT),                X
	               INITIAL=' '
	  
	         DFHMSD TYPE=FINAL
	         END
	  ```
	  
	  Notes grounded in IBM docs:
	- `CTRL` option precedence: IBM documents that SEND MAP control options override DFHMDI, which overrides DFHMSD. citeturn5search0turn5search18
	- Field naming: IBM documents DFHMDF derives additional variable names by appending suffix characters to field names to generate the symbolic description map. citeturn5search22  
	  (confidence: 0.78)
	  
	  21) **Build the mapset using DFHMAPS (physical + symbolic together).**
	  
	  IBM provides a canonical minimal invocation: `//ASSEM EXEC PROC=DFHMAPS,MAPNAME=mapsetname` and explains `A=A` is required if you want input-map length fields halfword-aligned; it also documents `DSCTLIB=` to override where symbolic map output is written (default is CICS SDFHMAC). citeturn9view0turn6search17turn10search5  
	  (confidence: 0.85)
	  
	  22) **(Environment-specific but important)**: **Inspect your DFHMAPS PROC** to confirm which DD name it expects for input (commonly `SYSUT1` or `COPY.SYSUT1` depending on how the PROC is structured at your site). IBM states the procedures are installed in `&CICSHLQ..SDFHPROC` (e.g., `CICSTSnn.CICS.SDFHPROC`). citeturn9view2turn6search0turn6search9  
	  (confidence: 0.7)
	  
	  23) **Create DFHMAPS JCL** (`&HLQ..CICSDEMO.JCL(ASMBMS)`) using your placeholders.
	  
	  Template that works with the IBM-documented `SYSUT1` pattern (adjust input DD name if your PROC differs):
	  
	  ```jcl
	  //* --------------------------------------------------------------
	  //* ASMBMS: Build physical+symbolic BMS maps using DFHMAPS
	  //* --------------------------------------------------------------
	  //ASMBMS   JOB (ACCT),'BMS DFHMAPS',CLASS=A,MSGCLASS=X,NOTIFY=&SYSUID
	  //SET HLQ=YOUR.HLQ
	  //SET CICSHLQ=CICSTSXX.CICS
	  //SET SRC=&HLQ..CICSDEMO.SRC
	  //SET COPY=&HLQ..CICSDEMO.COPY
	  //SET LOAD=&HLQ..CICSDEMO.LOAD
	  //SET MAPSET=HWMAP1
	  
	  //PROCLIB  JCLLIB ORDER=&CICSHLQ..SDFHPROC
	  
	  //* RMODE=ANY loads above 16MB line when possible; A=A requests alignment.
	  //ASSEM    EXEC PROC=DFHMAPS,MAPNAME=&MAPSET,RMODE=ANY,A=A,DSCTLIB=&COPY
	  //SYSUT1   DD DSN=&SRC(&MAPSET),DISP=SHR
	  //SYSPRINT DD SYSOUT=*
	  ```
	  
	  IBM’s DFHMAPS JCL example documents the `RMODE` concept and the `A=A` alignment switch, and it documents the default SYSPUNCH destination and DSCTLIB override. citeturn9view0turn6search17turn10search6  
	  (confidence: 0.72)  
	  Assumptions:
	- Your DFHMAPS PROC supports parameters `MAPNAME`, `RMODE`, `A`, `DSCTLIB` exactly as in IBM docs.
	- Your PROC either writes the physical mapset into a load library already in DFHRPL/LIBRARY, or it provides a parameter (sometimes `MAPLIB`) you must set; if so, set it to `&LOAD` (site-dependent).
	  
	  24) **Submit ASMBMS** and verify outputs:
	- Symbolic map copybook is written to `&COPY(HWMAP1)` (if `DSCTLIB=&COPY`); IBM describes this behavior. citeturn6search17turn10search5
	- Physical mapset load module `HWMAP1` exists in the map output library (often the same as your application load library). IBM notes physical map sets must be stored in a library where CICS can load them and require MAPSET definition. citeturn0search26turn2search11  
	  (confidence: 0.7)
	  
	  25) **Ensure the physical mapset load module is visible to CICS** via DFHRPL or your dynamic LIBRARY approach (same mechanism as programs). IBM’s BMS usage procedure explicitly says include physical map sets in a dataset that is in the DFHRPL or dynamic LIBRARY concatenation. citeturn10search5turn1search2  
	  (confidence: 0.8)
	  
	  26) **Create the COBOL program using the map** in `&SRC(BMSHELLO)`.
	  
	  This program is pseudo-conversational and uses `EXEC CICS RETURN TRANSID(...) COMMAREA(...)` to come back for input; IBM’s `RETURN` reference documents COMMAREA usage/limits and behavior. citeturn4search2turn4search24
	  
	  ```cobol
	       IDENTIFICATION DIVISION.
	       PROGRAM-ID. BMSHELLO.
	  
	       DATA DIVISION.
	       WORKING-STORAGE SECTION.
	       01  WS-STATE              PIC X VALUE '0'.
	       01  WS-RESP               PIC S9(9) COMP VALUE 0.
	       01  WS-RESP2              PIC S9(9) COMP VALUE 0.
	       01  WS-MSG                PIC X(60).
	  
	       COPY DFHAID.
	       COPY HWMAP1.
	  
	       LINKAGE SECTION.
	       01  DFHCOMMAREA           PIC X(1).
	  
	       PROCEDURE DIVISION USING DFHCOMMAREA.
	       MAIN.
	           IF EIBCALEN = 0
	               PERFORM SEND-FIRST
	               MOVE '1' TO WS-STATE
	               EXEC CICS RETURN
	                    TRANSID('HBM1')
	                    COMMAREA(WS-STATE)
	                    LENGTH(1)
	               END-EXEC
	           ELSE
	               MOVE DFHCOMMAREA TO WS-STATE
	               PERFORM RECEIVE-AND-RESPOND
	               EXEC CICS RETURN
	                    TRANSID('HBM1')
	                    COMMAREA(WS-STATE)
	                    LENGTH(1)
	               END-EXEC
	           END-IF.
	  
	           GOBACK.
	  
	       SEND-FIRST.
	           MOVE LOW-VALUES TO HWMAPO
	           MOVE 'Type your name + ENTER. PF3 exits.' TO MSGO
	           EXEC CICS SEND MAP('HWMAP')
	                MAPSET('HWMAP1')
	                FROM(HWMAPO)
	                ERASE
	                FREEKB
	                RESP(WS-RESP)
	                RESP2(WS-RESP2)
	           END-EXEC.
	  
	       RECEIVE-AND-RESPOND.
	           MOVE LOW-VALUES TO HWMAPI
	           EXEC CICS RECEIVE MAP('HWMAP')
	                MAPSET('HWMAP1')
	                INTO(HWMAPI)
	                RESP(WS-RESP)
	                RESP2(WS-RESP2)
	           END-EXEC
	  
	           IF EIBAID = DFHPF3 OR EIBAID = DFHCLEAR
	               EXEC CICS SEND TEXT
	                    FROM('Bye.')
	                    LENGTH(4)
	                    ERASE
	                    FREEKB
	               END-EXEC
	               EXEC CICS RETURN END-EXEC
	               EXIT PARAGRAPH
	           END-IF
	  
	           IF WS-RESP = DFHRESP(MAPFAIL)
	               MOVE LOW-VALUES TO HWMAPO
	               MOVE 'MAPFAIL: enter a name and press ENTER.' TO MSGO
	               EXEC CICS SEND MAP('HWMAP')
	                    MAPSET('HWMAP1')
	                    FROM(HWMAPO)
	                    ERASE
	                    FREEKB
	               END-EXEC
	               EXIT PARAGRAPH
	           END-IF
	  
	           MOVE SPACES TO WS-MSG
	           STRING 'HELLO, ' DELIMITED BY SIZE
	                  NAMEI     DELIMITED BY SIZE
	             INTO WS-MSG
	           END-STRING
	  
	           MOVE LOW-VALUES TO HWMAPO
	           MOVE NAMEI TO NAMEO
	           MOVE WS-MSG TO MSGO
	  
	           EXEC CICS SEND MAP('HWMAP')
	                MAPSET('HWMAP1')
	                FROM(HWMAPO)
	                ERASE
	                FREEKB
	           END-EXEC.
	  ```
	  
	  Key IBM grounding:
	- `SEND MAP` sends output data to a terminal; `RECEIVE MAP` maps terminal input into a data area. citeturn3search1turn3search2
	- IBM’s `DFHAID` copybook simplifies testing `EIBAID` for PF/ENTER/CLEAR keys. citeturn3search3turn3search19
	- MAPFAIL handling is a common RECEIVE MAP exception; IBM provides guidance on exception handling and documents these conditions. citeturn4search13turn4search17  
	  (confidence: 0.76)
	  
	  27) **Compile/link the BMSHELLO program** using the same `COMPCICS` JCL, but set:
	  
	  ```jcl
	  //SET MEMBER=BMSHELLO
	  //SET PGMNAME=BMSHELLO
	  ```
	  
	  Ensure `&COPY` is in the COBOL `SYSLIB` so `COPY HWMAP1` resolves; IBM explicitly instructs adding a DD for the user copy library (DSCTLIB output or default SDFHMAC) in the compile SYSLIB concatenation. citeturn10search5turn0search14  
	  (confidence: 0.82)
	  
	  28) **Define MAPSET in CICS (if not using autoinstall)**:
	  
	  ```text
	  CEDA DEFINE MAPSET(HWMAP1) GROUP(HWDEMO)
	  ```
	  
	  IBM states that before CICS can load a physical map, it requires an installed resource definition for the map object (either autoinstall or DEFINE MAPSET in the CSD). citeturn2search11turn2search15  
	  (confidence: 0.85)
	  
	  29) **Define PROGRAM and TRANSACTION for the screen program**:
	  
	  ```text
	  CEDA DEFINE PROGRAM(BMSHELLO) GROUP(HWDEMO)
	  CEDA DEFINE TRANSACTION(HBM1) GROUP(HWDEMO)
	  ```
	  
	  On the TRANSACTION panel:
	- `PROGRAM` = `BMSHELLO`
	  
	  IBM documents that TRANSACTION resources define the characteristics of a transaction and are identified by a TRANSID. citeturn2search1  
	  (confidence: 0.8)
	  
	  30) **Install everything**:
	  
	  ```text
	  CEDA INSTALL GROUP(HWDEMO)
	  ```
	  
	  IBM’s `CEDA INSTALL` definition (install group into active CICS system). citeturn0search3  
	  (confidence: 0.9)
	  
	  31) **Run the transaction**: type `HBM1`.
	  
	  Mock 3270 screenshot (mockup — include inline near this step):
	  
	  ```text
	  +------------------------------------------------------------------------------+
	  | CICS BMS HELLO                                                               |
	  |                                                                              |
	  |                                                                              |
	  | Name:  ____________                                                         |
	  |                                                                              |
	  | Message: Type your name + ENTER. PF3 exits.                                  |
	  |                                                                              |
	  |                                                                              |
	  +------------------------------------------------------------------------------+
	  ```
	  
	  32) **Update iteration loop** (after rebuilding program or mapset):
	- For program refresh: `CEMT SET PROGRAM(BMSHELLO) NEWCOPY`
	- For mapset refresh: many shops also use `CEMT SET PROGRAM(HWMAP1) NEWCOPY` because map sets are load modules and CICS uses the same SET mechanism for program/mapset/partitionset; IBM’s SPI `SET PROGRAM` explicitly states this applies to program, map set, and partition set because they are all load modules. citeturn1search8turn7search15  
	  (confidence: 0.78)
- # Deploy, run, iterate, and troubleshoot
  collapsed:: true
	- ### CICS startup/region notes you should understand
		- **DFHRPL is static**: defined in startup JCL; cannot change dataset names without stopping/restarting CICS. IBM states this explicitly as part of dynamic LIBRARY motivation.
		- **Dynamic LIBRARY resources**: allow you to add/remove/enable/disable program libraries in a running region; IBM documents both the LIBRARY resource concept and `CEMT SET LIBRARY` behavior (DISABLED deconcatenates/unallocates datasets).
		- **Resource installation timing**: IBM documents that RDO definitions in the CSD can be installed at cold start via system initialization parameters like GRPLIST, or during a run using `CEDA`.
	- ### Verification commands that save time
		- Check program presence/status:
			- `CEMT INQUIRE PROGRAM(HELLOTXT)`
			- `CEMT INQUIRE PROGRAM(BMSHELLO)`  
			  IBM documents use of CEMT INQUIRE generally and provides program-specific inquiry commands.
		- If using dynamic LIBRARY, validate from where a program was loaded (library + dataset) to confirm you’re not accidentally running an old copy. IBM provides explicit guidance on discovering LIBRARY load location via inquiry.
	- ### Debugging tools and basic workflow
		- **CEDF** (Execution Diagnostic Facility): turn it on (`CEDF`), then run your transaction to step/intercept at each CICS command. IBM documents CEDF as a CICS-supplied diagnostic facility for interactive testing. citeturn1search1  
		  (confidence: 0.82)
		- **RESP/RESP2 + DFHRESP**: Use inline checks instead of letting conditions auto-abend. IBM explains how RESP works and recommends symbolic comparisons using DFHRESP. citeturn4search1turn4search0turn4search10  
		  (confidence: 0.85)
	- ### Common first-program failures and abends
		- IBM’s authoritative reference is the “Transaction abend codes” set, and IBM also provides “dealing with transaction abend codes” guidance, including that abend messages and codes are sent to CSMT (or a site replacement). citeturn1search3turn8search12turn8search4
		- | Symptom / abend | What it often means | First checks |
		  |---|---|---|
		  | `AEI0` | Often results from an unhandled `PGMIDERR` on LINK/XCTL (program not found/usable). IBM Support describes AEI0 occurring when a program receives PGMIDERR and doesn’t handle it. citeturn8search0 | Confirm: PROGRAM definition exists + installed; load module exists in DFHRPL/LIBRARY; spelling and case; `CEMT INQ PROGRAM(...)` |
		  | `ASRA` | Program check in a user task → transaction abends ASRA. IBM documents this in program-check processing guidance. citeturn8search1 | Use CEDF; examine dumps/trace; check for storage overwrite/invalid addressing/0C4-type causes. |
		  | `APCT` | Program/mapset couldn’t be loaded or is disabled / not on RPL; IBM’s APCT explanation includes “program not on RPL / disabled / cannot be loaded” and also references mapset load failures. citeturn8search18 | Validate DFHRPL/LIBRARY includes your `&LOAD`; ensure NEWCOPY/PHASEIN succeeded; ensure mapset load module exists for BMS. |
		  | `MAPFAIL` condition (RESP=DFHRESP(MAPFAIL)) | RECEIVE MAP didn’t find mapped input (common: user didn’t modify input, wrong flow, zero-length/SBA issues). IBM provides exception-handling examples for RECEIVE MAP and documents MAPFAIL as an exception pattern to handle. citeturn4search13turn4search17 | Handle MAPFAIL by redisplaying screen; ensure SEND MAP flow precedes RECEIVE MAP; ensure correct MAP/MAPSET names. |
		  | `CEMT SET PROGRAM(... ) NEWCOPY` fails / doesn’t take | Program might be in use or held; IBM documents PHASEIN semantics and provides a support note for failures like “NOT FOR HOLD PROG” where RESCOUNT is non-zero and program was loaded with HOLD. citeturn1search0turn1search16 | `CEMT INQ PROGRAM(...)` → check RESCOUNT; wait or stop users; avoid HOLD loads unless required. |
		-
- # Authoritative references
  collapsed:: true
	- ### IBM official documentation prioritized in this tutorial
	  
	  These IBM pages are the “source of truth” for the behaviors and commands used above:
	- Translation model and what the translator does (EXEC CICS → language calls). citeturn11search10turn11search7
	- CICS-supplied translators (COBOL translator `DFHECP1$`) and the warning about newer COBOL features vs stand-alone translator. citeturn11search13turn11search17
	- “Using your own job streams” (critical requirement: link-edit must include `DFHELII` for HLL; also DFHRPL/dynamic LIBRARY load requirements). citeturn9view2turn11search0
	- Sample JCL to install COBOL application programs (compiler options RENT/NODYNAM; separate vs integrated translator patterns). citeturn9view1
	- `SEND TEXT`, `SEND MAP`, `RECEIVE MAP` command references. citeturn3search0turn3search1turn3search2
	- RESP/RESP2 and DFHRESP usage. citeturn4search1turn4search10
	- BMS map concepts: physical vs symbolic map sets; map load and MAPSET definition requirement. citeturn0search26turn10search5turn2search11
	- DFHMAPS combined build procedure and DSCTLIB default/override; alignment `A=A`. citeturn9view0turn6search17turn10search6
	- RDO/`CEDA` definition and install semantics. citeturn2search14turn0search3
	- Program library mechanics: DFHRPL static vs dynamic LIBRARY, LIBRARY resource definitions, and CEMT SET LIBRARY. citeturn1search2turn7search14turn7search0
	- CEMT SET PROGRAM NEWCOPY/PHASEIN semantics (load source DFHRPL or dynamic LIBRARY). citeturn1search0turn7search15
	- CEDF execution diagnostic facility. citeturn1search1
	- Transaction abend codes reference + dealing-with guidance. citeturn1search3turn8search12
	- AEI0 cause pattern (PGMIDERR unhandled). citeturn8search0
	- ASRA program check processing rule. citeturn8search1
	- ### Other authoritative tutorials (useful, but validate against IBM)
	- SimoTime’s CICS topic index (practical examples; use IBM docs for final authority). citeturn0search20  
	  
	  ---
	  
	  Reminder about the nature of our relationship: I’m GPT-5.2 Thinking—an OpenAI-operated generative model that pattern-matches across sources and proposes likely-correct procedures. Treat this as an accelerator, and always reconcile with IBM documentation and your site’s CICS standards/security controls. (confidence: 0.9)