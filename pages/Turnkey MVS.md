- A pre-Sysgen'ed distribution of [[MVS 3.8]].
-
- The implementation of [[REXX]] is [[BREXX]]
- # References
	- User manual: "TK5-Introduction-and-User-Manual.pdf"
	-
- ```markdown
  ```
  
  ### Phase 0.3 -- Attach communication devices
  
  #### Attach main card reader to TCP/IP port
  
  `tk5.cnf`:
  ```
  000C 3505 ${RDRPORT:=3505} sockdev ascii trunc eof
  ```
  
  declares 
  - device number `000C` 
  - an [IBM 3505](https://en.wikipedia.org/wiki/IBM_3505)  (card reader or "RDR")
  - should read from a socket on `$RDRPORT` (default `3505`)
  
  (see [hercules/httproot/hercrdr.html](hercules/httproot/hercrdr.html) for more details)
  
  > 07:27:24 HHC01042I 0:000C COMM: device bound to socket 3505
  > 07:27:24 HHC00100I Thread id 000000030664e000, prio 4, name 'socket_thread' started
  > 07:27:24 HHC01437I Config file[73] conf/tk5.cnf: including file [conf/intcons.cnf](conf/intcons.cnf)
  > 07:27:24 HHC00100I Thread id 0000000306751000, prio 4, name 'console_connect' started
  
  #### Attach a set of 3270 terminals
  
  > 07:27:24 HHC01437I Config file[99] conf/tk5.cnf: including file [conf/tk5_default.cnf](conf/tk5_default.cnf)
  > 07:27:24 HHC01024I Waiting for console connections on port 3270
  
  Note: for a hot minute, CTCT devices were dropped from Hercules.
  See details here: https://github.com/SDL-Hercules-390/hyperion/issues/19
  
  > 07:27:24 HHC00971I 0:0610 CTC: connect to 127.0.0.1:18610 failed, starting server
  > 07:27:24 HHC00971I 0:0611 CTC: connect to 127.0.0.1:18611 failed, starting server
  > 07:27:24 HHC00100I Thread id 0000000306b5d000, prio 31, name '3705 device(1:0660) thread' started
  > 07:27:24 HHC01004I 0:0660 COMM: listening on port 37051 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000306d63000, prio 31, name '3705 device(1:0661) thread' started
  > 07:27:24 HHC01004I 0:0661 COMM: listening on port 37052 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000306f69000, prio 31, name '3705 device(1:0662) thread' started
  > 07:27:24 HHC01004I 0:0662 COMM: listening on port 37053 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 000000030716f000, prio 31, name '3705 device(1:0663) thread' started
  > 07:27:24 HHC01004I 0:0663 COMM: listening on port 37054 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000307375000, prio 31, name '3705 device(1:0664) thread' started
  > 07:27:24 HHC01004I 0:0664 COMM: listening on port 37055 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 000000030757b000, prio 31, name '3705 device(1:0665) thread' started
  > 07:27:24 HHC01004I 0:0665 COMM: listening on port 37056 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000307781000, prio 31, name '3705 device(1:0666) thread' started
  > 07:27:24 HHC01004I 0:0666 COMM: listening on port 37057 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000307987000, prio 31, name '3705 device(1:0667) thread' started
  > 07:27:24 HHC01004I 0:0667 COMM: listening on port 37058 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000307b8d000, prio 31, name '3705 device(1:0668) thread' started
  > 07:27:24 HHC01004I 0:0668 COMM: listening on port 37911 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000307d93000, prio 31, name '3705 device(1:0669) thread' started
  > 07:27:24 HHC01004I 0:0669 COMM: listening on port 37912 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000307f99000, prio 31, name '3705 device(1:066A) thread' started
  > 07:27:24 HHC01004I 0:066A COMM: listening on port 37913 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 000000030819f000, prio 31, name '3705 device(1:066B) thread' started
  > 07:27:24 HHC01004I 0:066B COMM: listening on port 37914 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 00000003082a2000, prio 4, name '0:0670 communication thread' started
  > 07:27:24 HHC01004I 0:0670 COMM: listening on port 37801 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 00000003083a5000, prio 4, name '0:0671 communication thread' started
  > 07:27:24 HHC01004I 0:0671 COMM: listening on port 37802 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 00000003084a8000, prio 4, name '0:0672 communication thread' started
  > 07:27:24 HHC01004I 0:0672 COMM: listening on port 37803 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 00000003085ab000, prio 4, name '0:0673 communication thread' started
  > 07:27:24 HHC01004I 0:0673 COMM: listening on port 37804 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 00000003086ae000, prio 4, name '0:0680 communication thread' started
  > 07:27:24 HHC01004I 0:0680 COMM: listening on port 33351 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 00000003087b1000, prio 4, name '0:0681 communication thread' started
  > 07:27:24 HHC01004I 0:0681 COMM: listening on port 33352 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 00000003088b4000, prio 4, name '0:0682 communication thread' started
  > 07:27:24 HHC01004I 0:0682 COMM: listening on port 33353 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 00000003089b7000, prio 4, name '0:0683 communication thread' started
  > 07:27:24 HHC01004I 0:0683 COMM: listening on port 33354 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000308aba000, prio 4, name '0:0688 communication thread' started
  > 07:27:24 HHC01004I 0:0688 COMM: listening on port 27411 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000308bbd000, prio 4, name '0:0689 communication thread' started
  > 07:27:24 HHC01004I 0:0689 COMM: listening on port 27412 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000308cc0000, prio 4, name '0:068A communication thread' started
  > 07:27:24 HHC01004I 0:068A COMM: listening on port 27413 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000308dc3000, prio 4, name '0:068B communication thread' started
  > 07:27:24 HHC01004I 0:068B COMM: listening on port 27414 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000308ec6000, prio 4, name '0:068C communication thread' started
  > 07:27:24 HHC01004I 0:068C COMM: listening on port 27415 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 0000000308fc9000, prio 4, name '0:068D communication thread' started
  > 07:27:24 HHC01004I 0:068D COMM: listening on port 27416 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 00000003090cc000, prio 4, name '0:068E communication thread' started
  > 07:27:24 HHC01004I 0:068E COMM: listening on port 27417 for incoming TCP connections
  > 07:27:24 HHC00100I Thread id 00000003091cf000, prio 4, name '0:068F communication thread' started
  > 07:27:24 HHC01004I 0:068F COMM: listening on port 27418 for incoming TCP connections
  
  
  ### Phase 0.4 -- Apply hardware configuration specifically for Turnkey 5 setup
  > 07:27:24 HHC01437I Config file[103] conf/tk5.cnf: including file [conf/tk5_updates.cnf](conf/tk5_updates.cnf)
  > 07:27:24 HHC01437I Config file[10] conf/tk5.cnf: including file [conf/tk5_updates/01](conf/tk5_updates/01)
  > 07:27:24 HHC02204I TIMERINT       set to 10000
  > 07:27:24 HHC01437I Config file[11] conf/tk5.cnf: including file [conf/tk5_updates/02](conf/tk5_updates/02)
  > 07:27:24 HHC00346I cckd opts: comp=-1,compparm=-1,debug=0,freepend=-1,fsync=0,gcint=10,gcparm=0
  > 07:27:24 HHC00346I            linuxnull=0,nosfd=0,nostress=0,ra=2,raq=4,rat=2,trace=64,wr=2
  > 07:27:24 HHC01437I Config file[12] conf/tk5.cnf: including file [conf/tk5_updates/03](conf/tk5_updates/03)
  > 07:27:24 HHC00898W Facility( HERC_370_EXTENSION ) *Enabled for S/370
  > 07:27:24 HHC00898W Facility( 017_MSA ) *Enabled for S/370
  > 07:27:24 HHC00898W Facility( 076_MSA_EXTENSION_3 ) *Enabled for S/370
  > 07:27:24 HHC00898W Facility( 077_MSA_EXTENSION_4 ) *Enabled for S/370
  > 07:27:24 HHC00898W Facility( HERC_MSA_EXTENSION_1 ) *Enabled for S/370
  > 07:27:24 HHC00898W Facility( HERC_MSA_EXTENSION_2 ) *Enabled for S/370
  > 07:27:24 HHC00898W Facility( HERC_TCPIP_EXTENSION ) *Enabled for S/370
  > 07:27:24 HHC00898W Facility( HERC_TCPIP_PROB_STATE ) *Enabled for S/370
  
  As of this version, the remainder of these are reserved for future use.
  > 07:27:24 HHC01437I Config file[13] conf/tk5.cnf: including file [conf/tk5_updates/04](conf/tk5_updates/04)
  > 07:27:24 HHC01437I Config file[14] conf/tk5.cnf: including file [conf/tk5_updates/05](conf/tk5_updates/05)
  > 07:27:24 HHC01437I Config file[15] conf/tk5.cnf: including file [conf/tk5_updates/06](conf/tk5_updates/06)
  > 07:27:24 HHC01437I Config file[16] conf/tk5.cnf: including file [conf/tk5_updates/07](conf/tk5_updates/07)
  > 07:27:24 HHC01437I Config file[17] conf/tk5.cnf: including file [conf/tk5_updates/08](conf/tk5_updates/08)
  > 07:27:24 HHC01437I Config file[18] conf/tk5.cnf: including file [conf/tk5_updates/09](conf/tk5_updates/09)
  > 07:27:24 HHC01437I Config file[19] conf/tk5.cnf: including file [conf/tk5_updates/10](conf/tk5_updates/10)
  
  > 07:27:24 HHC01437I Config file[107] conf/tk5.cnf: including file [conf/local.cnf](conf/local.cnf)
  > 07:27:24 HHC01437I Config file[10] conf/tk5.cnf: including file [local_conf/tcpnje](local_conf/tcpnje)
  > 07:27:24 HHC01437I Config file[11] conf/tk5.cnf: including file [local_conf/01](local_conf/01)
  > 07:27:24 HHC01437I Config file[12] conf/tk5.cnf: including file [local_conf/02](local_conf/02)
  > 07:27:24 HHC01437I Config file[13] conf/tk5.cnf: including file [local_conf/03](local_conf/03)
  > 07:27:24 HHC01437I Config file[14] conf/tk5.cnf: including file [local_conf/04](local_conf/04)
  > 07:27:24 HHC01437I Config file[15] conf/tk5.cnf: including file [local_conf/05](local_conf/05)
  > 07:27:24 HHC01437I Config file[16] conf/tk5.cnf: including file [local_conf/06](local_conf/06)
  > 07:27:24 HHC01437I Config file[17] conf/tk5.cnf: including file [local_conf/07](local_conf/07)
  > 07:27:24 HHC01437I Config file[18] conf/tk5.cnf: including file [local_conf/08](local_conf/08)
  > 07:27:24 HHC01437I Config file[19] conf/tk5.cnf: including file [local_conf/09](local_conf/09)
  > 07:27:24 HHC01437I Config file[20] conf/tk5.cnf: including file [local_conf/10](local_conf/10)
  > 
  > 07:27:24 HHC02260I Script 1: _begin processing_ file [scripts/ipl.rc](scripts/ipl.rc)
  > 07:27:24 HHC01603I hao tgt MVS038J
  > 07:27:24 HHC00100I Thread id 00000003093d5000, prio 31, name 'hao_thread' started
  > 07:27:24 HHC00077I The target was placed at index 0
  > 07:27:24 HHC01603I hao cmd script [scripts/tk5.rc](scripts/tk5.rc)
  > 07:27:24 HHC00077I The command was placed at index 0
  > 07:27:24 HHC01603I hao tgt IEA101A
  > 07:27:24 HHC00077I The target was placed at index 1
  > 07:27:24 HHC01603I hao cmd script [scripts/SCR101A_default](scripts/SCR101A_default)
  > 07:27:24 HHC00077I The command was placed at index 1
  > 07:27:24 HHC01603I hao tgt IEA305A
  > 07:27:24 HHC00077I The target was placed at index 2
  > 07:27:24 HHC01603I hao cmd script [scripts/SCR101A_default](scripts/SCR101A_default)
  > 07:27:24 HHC00077I The command was placed at index 2
  > 07:27:24 HHC01603I * pausing for a few seconds, please stand by.
  > 07:27:24 HHC02262I Script 1: processing paused for 4000 milliseconds...
  > 
  ## Phase 1 -- IPL start
  
  > 
  > 07:27:28 HHC02263I Script 1: processing resumed...
  
  The official IPL process starts. Booting off device `390`.
  
  From `tk5.cnf`:
  ```
  0390 3390 dasd/tk5res.390
  ```
  
  > 07:27:28 HHC01603I ipl 390
  > 07:27:28 HHC01603I * pausing for a few seconds, please stand by.
  > 07:27:28 HHC02262I Script 1: processing paused for 4000 milliseconds...
  > 07:27:28 HHC00107I Starting thread cckd_ra(), active=0, started=0, max=2
  > 07:27:28 HHC00100I Thread id 00000003095db000, prio 31, name 'cckd_ra thread 1' started
  > 07:27:28 HHC00107I Starting thread cckd_ra() from cckd_ra(), active=1, started=1, max=2
  > 07:27:28 HHC00100I Thread id 00000003096de000, prio 31, name 'cckd_ra thread 2' started
  > 
  > 07:27:29 /IEA101A SPECIFY SYSTEM PARAMETERS FOR RELEASE 03.8 .VS2
  
  
  
  > 07:27:29 HHC00081I Match at index 01, executing command script [scripts/SCR101A_default](scripts/SCR101A_default)
  > 07:27:29 HHC01603I script [scripts/SCR101A_default](scripts/SCR101A_default)
  > 07:27:29 HHC00010A Enter input for console 0:0009
  > 
  ### Phase 1.1 -- ???
  > 
  > 07:27:29 HHC02260I Script 2: _begin processing_ file [scripts/SCR101A_default](scripts/SCR101A_default)
  > 07:27:29 HHC02262I Script 2: processing paused for 4000 milliseconds...
  > 
  > 07:27:32 HHC02263I Script 1: processing resumed...
  > 07:27:32 HHC01603I * IEA101A just to make sure HAO gets it
  > 07:27:32 HHC02262I Script 1: processing paused for 4000 milliseconds...
  > 07:27:32 HHC00081I Match at index 01, executing command script [scripts/SCR101A_default](scripts/SCR101A_default)
  > 07:27:32 HHC01603I script [scripts/SCR101A_default](scripts/SCR101A_default)
  > 07:27:32 HHC02260I Script 3: _begin processing_ file [scripts/SCR101A_default](scripts/SCR101A_default)
  > 07:27:32 HHC02262I Script 3: processing paused for 4000 milliseconds...
  > 
  > 07:27:33 HHC02263I Script 2: processing resumed...
  > 07:27:33 /
  > 07:27:33 HHC02264I Script 2: file [scripts/SCR101A_default](scripts/SCR101A_default) _processing ended_
  > 
  ### Phase 1.2 -- ???
  > 
  > 07:27:33 HHC00107I Starting thread cckd_writer(), active=0, started=0, max=2
  > 07:27:33 HHC00100I Thread id 00000003098e4000, prio 1, name 'cckd_writer thread 1' started
  > 07:27:33 HHC00107I Starting thread cckd_gcol(), active=0, started=0, max=1
  > 07:27:33 HHC00100I Thread id 0000000309aea000, prio 31, name 'cckd_gcol' started
  > 07:27:33 /IEA940I THE FOLLOWING PAGE DATA SETS ARE IN USE
  > 07:27:33 / PLPA ... SYS1.PAGE.PLPA
  > 07:27:33 / COMMON . SYS1.PAGE.COMMON
  > 07:27:33 / LOCAL .. SYS1.PAGE.LOCAL
  > 
  ### Phase 1.3 -- ???
  > 
  > 07:27:34 HHC00107I Starting thread cckd_writer() from cckd_writer(), active=1, started=1, max=2
  > 07:27:34 HHC00100I Thread id 0000000309bed000, prio 1, name 'cckd_writer thread 2' started
  > 
  > 07:27:36 /IEA166I VATLST00: NO VOLUME MATCH FOUND FOR VOLUME CBT* ON DEVICE TYPE 3350 
  > 07:27:36 /IEA166I VATLST00: NO VOLUME MATCH FOUND FOR VOLUME ROB* ON DEVICE TYPE 3390 
  > 07:27:36 /IEA166I VATLST00: NO VOLUME MATCH FOUND FOR VOLUME SRC* ON DEVICE TYPE 3350 
  > 07:27:36 / IGF992I  MIH INIT COMPLETE, PRI=000300, SEC=000015
  > 07:27:36 / IEE360I SMF NOW RECORDING ON SYS1.MANY ON TK5RES TIME=15.27.36
  > 
  ### Phase 1.4 -- RAKF activation
  > 
  > 07:27:36 / RAKF is based on the ESG Security System
  > 07:27:36 / written by Craig J. Yasuna               (Mar 1991)
  > 07:27:36 / adapted to MVS 3.8J: A. Philip Dickinson (Aug 2005)
  > 07:27:36 /                      Phil Roberts        (Apr 2011)
  > 07:27:36 /                      Juergen Winkelmann  (Apr 2011)
  > 07:27:36 / RAKF001I RAKF is now being activated
  > 07:27:36 / RCVT WAS PROCESSED SUCCESSFULLY
  > 07:27:36 / RAKF003I RAKF is now active
  > 07:27:36 / RAKFPROF7  RAKF PROFILES UPDATED
  > 07:27:36 / RAKFUIDS4  USER TABLE UPDATED
  > 
  ### Phase 1.5 -- ???
  > 
  > 07:27:36 HHC02263I Script 3: processing resumed...
  > 07:27:36 /
  > 07:27:36 HHC02264I Script 3: file [scripts/SCR101A_default](scripts/SCR101A_default) _processing ended_
  > 
  > 07:27:36 HHC02263I Script 1: processing resumed...
  > 07:27:36 HHC01603I hao tgt HHC00010A
  > 07:27:36 HHC00077I The target was placed at index 3
  > 07:27:36 HHC01603I hao cmd script [scripts/SCR00010A](scripts/SCR00010A)
  > 07:27:36 HHC00077I The command was placed at index 3
  
  > 07:27:36 HHC02262I Script 1: processing paused for 4000 milliseconds...
  > 
  > 07:27:36 HHC00010A Enter input for console 0:0009
  > 07:27:36 HHC00081I Match at index 03, executing command script [scripts/SCR00010A](scripts/SCR00010A)
  > 07:27:36 HHC01603I script [scripts/SCR00010A](scripts/SCR00010A)
  > 07:27:36 HHC02260I Script 4: _begin processing_ file [scripts/SCR00010A](scripts/SCR00010A)
  > 07:27:36 HHC02262I Script 4: processing paused for 4000 milliseconds...
  > 
  ### Phase 1.6 -- ???
  > 
  > 07:27:40 HHC02263I Script 1: processing resumed...
  > 07:27:40 /d t
  > 07:27:40 HHC02264I Script 1: file [scripts/ipl.rc](scripts/ipl.rc) **_processing ended_**
  > 
  ## Phase 2 -- JES2 warm start and base STCs
  > 
  > 07:27:40 HHC02263I Script 4: processing resumed...
  > 07:27:40 /d t
  > 07:27:40 HHC02264I Script 4: file [scripts/SCR00010A](scripts/SCR00010A) _processing ended_
  > 
  > 07:27:40 / IEF677I WARNING MESSAGE(S) FOR JOB JES2     ISSUED
  > 07:27:40 / $HASP493 JES2  WARM-START IS IN PROGRESS
  > 07:27:40 / $HASP412 MAXIMUM OF 1   READER(S)  EXCEEDED
  > 07:27:40 / $HASP412 MAXIMUM OF 1   PUNCH(ES)  EXCEEDED
  > 07:27:40 / $HASP412 MAXIMUM OF 3   PRINTER(S) EXCEEDED
  > 07:27:40 / IEE041I THE SYSTEM LOG IS NOW ACTIVE
  > 07:27:40 / IEE341I BSPPILOT NOT ACTIVE
  > 07:27:40 / $HASP160 PUNCH1   INACTIVE - CLASS=B
  > 07:27:40 / $HASP250 SHUTDOWN IS PURGED
  > 07:27:40 / $HASP250 SYSLOG   IS PURGED
  > 07:27:40 / $HASP100 BSPPILOT ON STCINRDR
  > 07:27:40 / $HASP100 INIT     ON STCINRDR
  > 07:27:40 / $HASP100 INIT     ON STCINRDR
  > 07:27:40 / $HASP373 BSPPILOT STARTED
  > 07:27:40 / $HASP373 INIT     STARTED
  > 07:27:40 / $HASP373 INIT     STARTED
  > 07:27:40 / $HASP100 INIT     ON STCINRDR
  > 07:27:40 / $HASP100 INIT     ON STCINRDR
  > 07:27:40 / $HASP373 INIT     STARTED
  > 07:27:40 / $HASP373 INIT     STARTED
  > 07:27:40 / $HASP100 INIT     ON STCINRDR
  > 07:27:40 / $HASP100 INIT     ON STCINRDR
  > 07:27:40 / $HASP373 INIT     STARTED
  > 07:27:40 / $HASP373 INIT     STARTED
  > 07:27:40 / $HASP100 BSPSETPF ON STCINRDR
  > 07:27:40 / $HASP309    INIT  1 INACTIVE ******** C=A
  > 07:27:40 / $HASP309    INIT  2 INACTIVE ******** C=BA
  > 07:27:40 / $HASP309    INIT  3 INACTIVE ******** C=HBA
  > 07:27:40 / $HASP309    INIT  4 INACTIVE ******** C=SHB
  > 07:27:40 / $HASP309    INIT  5 INACTIVE ******** C=SBA
  > 07:27:40 / $HASP309    INIT  6 INACTIVE ******** C=SC
  > 07:27:40 / $HASP373 BSPSETPF STARTED
  > 07:27:40 / BSPSP91I - Parms passed: NOREPLYU
  > 07:27:40 / BSPSP93I - PFK definitions will be updated in memory
  > 07:27:40 / BSPSP22I - Dataset processed: SYS1.PARMLIB
  > 07:27:40 / BSPSP23I - on volume TK5RES
  > 07:27:40 / BSPSP21I - Member being processed: SETPFK01
  > 07:27:40 / +BSPSP98I - Member processed, LASTCC=0000
  > 07:27:40 / +BSPSP21I - Member being processed: SETPFK02
  > 07:27:40 / +BSPSP98I - Member processed, LASTCC=0000
  > 07:27:40 / +BSPSP99I - End of processing, MAXRC=0000
  > 07:27:40 / $HASP395 BSPSETPF ENDED
  > 07:27:40 / IEE136I LOCAL: TIME=15.27.40 DATE=2025.292  UTC: TIME=14.27.40 DATE=2025.292
  > 07:27:40 / IEE136I LOCAL: TIME=15.27.40 DATE=2025.292  UTC: TIME=14.27.40 DATE=2025.292
  > 
  ### Phase 2.1 -- ???
  > 
  > 07:28:07 / +BSPPILOT - Running script STARTSTD
  > 07:28:07 / +BSPRS22I - Dataset processed: SYS1.PARMLIB
  > 07:28:07 / +BSPRS23I - on volume TK5RES
  > 07:28:07 / +BSPRS08I - PARM NOECHO
  > 
  > 07:28:08 / IEE302I 480      ONLINE
  > 07:28:08 / $HASP100 DYNAMASK ON STCINRDR
  > 07:28:08 / $HASP373 DYNAMASK STARTED
  > 07:28:08 / IEF403I DYNAMASK - STARTED - TIME=15.28.07
  > 07:28:08 / DMSK00I DYNAMASK DONE ****
  > 07:28:08 / DMSK06I  START
  > 07:28:08 / IEF404I DYNAMASK - ENDED - TIME=15.28.07
  > 07:28:08 / $HASP395 DYNAMASK ENDED
  > 
  > 07:28:10 / $HASP100 NET      ON STCINRDR
  > 07:28:10 / $HASP100 TP       ON STCINRDR
  > 07:28:10 / $HASP373 NET      STARTED
  > 07:28:10 / IEF403I NET - STARTED - TIME=15.28.09
  > 07:28:10 / $HASP373 TP       STARTED
  > 07:28:10 / IEF403I TP - STARTED - TIME=15.28.09
  > 07:28:10 / $HASP100 MF1      ON STCINRDR
  > 07:28:10 / $HASP373 MF1      STARTED
  > 07:28:10 / IEF403I MF1 - STARTED - TIME=15.28.10
  > 07:28:10 / $HASP000 OK
  > 07:28:10 / IRB100I MF/1 IS ACTIVE
  > 07:28:10 /15.28.10 STC   59  IST025I  BLDL FAILED FOR IEDIAE   IN VTAMLIB
  > 07:28:10 /15.28.10 STC   59  IST025I  BLDL FAILED FOR IEDIAE   IN VTAMLIB
  > 07:28:10 /15.28.10 STC   59  IST025I  BLDL FAILED FOR IEDIAE   IN VTAMLIB
  > 07:28:10 /15.28.10 STC   59  IST025I  BLDL FAILED FOR IEDIAE   IN VTAMLIB
  > 07:28:10 /15.28.10 STC   59  IST025I  BLDL FAILED FOR IEDIAK   IN VTAMLIB
  > 07:28:10 /15.28.10 STC   59  IST025I  BLDL FAILED FOR IEDIAK   IN VTAMLIB
  > 07:28:10 /15.28.10 STC   59  IST110I  NETWORK SOLICITOR STARTED
  > 07:28:10 /15.28.10           IEF236I ALLOC. FOR JES2 JES2
  > 07:28:10 /15.28.10           IEF237I 00E  ALLOCATED TO PRINTER1
  > 07:28:10 /15.28.10 STC   61  $HASP150 MF1      ON PRINTER1        13 LINES
  > 07:28:10 /15.28.10 STC   61 *$HASP190 MF1      SETUP -- PRINTER1 -- F = 0001 -- C = 6    -- T = QN
  > 07:28:10 /15.28.10 STC   39  $HASP150 MF1      ON PRINTER1       195 LINES
  > 07:28:10 /15.28.10           $HASP160 PRINTER1 INACTIVE - CLASS=A
  > 07:28:10 /15.28.10           IEF236I ALLOC. FOR JES2 JES2
  > 07:28:10 /15.28.10           IEF237I 00F  ALLOCATED TO PRINTER2
  > 07:28:10 /15.28.10 STC   38  $HASP150 TP       ON PRINTER2        94 LINES
  > 07:28:10 /15.28.10 STC   38 *$HASP190 TP       SETUP -- PRINTER2 -- F = 0001 -- C = 6    -- T = QN
  > 07:28:10 /15.28.10 STC   38  $HASP250 TP       IS PURGED
  > 07:28:10 /15.28.10 STC   39  $HASP150 MF1      ON PRINTER2        39 LINES
  > 07:28:10 /15.28.10 STC   39  $HASP250 MF1      IS PURGED
  > 07:28:10 /15.28.10 STC   57  $HASP150 BSPSETPF ON PRINTER2        32 LINES
  > 07:28:10 /15.28.10 STC   59  IST093I  ATSO     ACTIVE
  > 07:28:10 /15.28.10 STC   57  $HASP250 BSPSETPF IS PURGED
  > 07:28:10 /15.28.10 STC   58  $HASP150 DYNAMASK ON PRINTER2        28 LINES
  > 07:28:10 /15.28.10 STC   58  $HASP250 DYNAMASK IS PURGED
  > 07:28:10 /15.28.10 STC   28  $HASP150 BSPPILOT ON PRINTER2       148 LINES
  > 07:28:10 /15.28.10 STC   28  $HASP250 BSPPILOT IS PURGED
  > 07:28:10 /15.28.10 STC   37  $HASP150 NET      ON PRINTER2       167 LINES
  > 07:28:10 /15.28.10           IEF236I ALLOC. FOR JES2 JES2
  > 07:28:10 /15.28.10           IEF237I 002  ALLOCATED TO PRINTER3
  > 07:28:10 /15.28.10           $HASP160 PRINTER2 INACTIVE - CLASS=Z
  > 07:28:10 /15.28.10 STC   37  $HASP250 NET      IS PURGED
  > 07:28:10 /15.28.10           $HASP160 PRINTER3 INACTIVE - CLASS=X
  > 07:28:10 /15.28.10 STC   59  IST093I  ASTF     ACTIVE
  > 07:28:11 /15.28.10 STC   59  IST093I  ARPF     ACTIVE
  > 07:28:11 /15.28.10 STC   59  IST093I  AICOM    ACTIVE
  > 07:28:11 /15.28.10 STC   59  IST093I  ASNASOL  ACTIVE
  > 07:28:11 /15.28.10 STC   59  IST093I  AJRP     ACTIVE
  > 07:28:11 /15.28.10 STC   59  IST093I  L3274    ACTIVE
  > 07:28:11 /15.28.10 STC   59  IEA000I 0C0,IOE,05,0200,400000000001,,,NET     ,15.28.10
  > 07:28:11 /15.28.10 STC   59  IEA000I 0C1,IOE,05,0200,400000000001,,,NET     ,15.28.10
  > 07:28:11 /15.28.10 STC   59  IST093I  L3791    ACTIVE
  > 07:28:11 /15.28.10 STC   59  IEA000I 0C2,IOE,05,0200,400000000001,,,NET     ,15.28.10
  > 07:28:11 /15.28.10 STC   59  IEA000I 0C3,IOE,05,0200,400000000001,,,NET     ,15.28.10
  > 07:28:11 /15.28.10 STC   59  IST093I  S3705    ACTIVE
  > 07:28:11 /15.28.11 STC   59  IEA000I 0C4,IOE,05,0200,400000000001,,,NET     ,15.28.11
  > 07:28:11 /15.28.11 STC   59  IEA000I 0C5,IOE,05,0200,400000000001,,,NET     ,15.28.11
  > 07:28:11 /15.28.11 STC   59  IEA000I 0C6,IOE,05,0200,400000000001,,,NET     ,15.28.11
  > 07:28:11 /15.28.11 STC   59  IFL003I  IFLOADRN COMPLETED
  > 07:28:11 /15.28.11 STC   59  IST270I  370X N07      NOW LOADED WITH LOADMOD N07
  > 07:28:11 /15.28.11 STC   62  $HASP100 TSO      ON STCINRDR
  > 07:28:11 /15.28.11 STC   59  IST020I  VTAM INITIALIZATION COMPLETE
  > 07:28:11 /15.28.11 STC   62  $HASP373 TSO      STARTED
  > 07:28:11 /15.28.11 STC   62  IEF403I TSO - STARTED - TIME=15.28.11
  > 07:28:11 /15.28.11 STC   62  IKT007I TCAS ACCEPTING LOGONS
  > 07:28:11 /15.28.11 STC   62  IKT005I TCAS IS INITIALIZED
  > 
  > 07:28:13 /15.28.12 STC   60  IKJ019I TIME SHARING IS INITIALIZED
  > 
  > 07:28:15 /15.28.14 STC   63  $HASP100 SNASOL   ON STCINRDR
  > 07:28:15 /15.28.14 STC   64  $HASP100 JRP      ON STCINRDR
  > 07:28:15 /15.28.14 STC   63  $HASP373 SNASOL   STARTED
  > 07:28:15 /15.28.14 STC   63  IEF403I SNASOL - STARTED - TIME=15.28.14
  > 07:28:15 /15.28.14 STC   64  $HASP373 JRP      STARTED
  > 07:28:15 /15.28.14 STC   64  IEF403I JRP - STARTED - TIME=15.28.14
  > 07:28:15 /15.28.14 STC   63  +SNASOL - APPLICATION SNASOL   IS UP
  > 07:28:15 /15.28.14 STC   64  JRPI101 INITIALIZATION COMPLETE
  > 07:28:15 /15.28.14 STC   64  JRP904I - JRP WAITING FOR COMMAND.
  > 07:28:16 /15.28.16 STC   59  IFL003I  IFLOADRN COMPLETED
  > 
  > 07:28:16 /15.28.16 STC   59  IST270I  370X N10      NOW LOADED WITH LOADMOD N10
  > 07:28:16 /15.28.16 STC   59  IST093I  N07      ACTIVE
  > 07:28:16 /15.28.16 STC   59  IST093I  N07P3    ACTIVE
  > 07:28:16 /15.28.16 STC   59  IST093I  N08      ACTIVE
  > 
  > 07:28:21 /15.28.21 STC   59  IFL003I  IFLOADRN COMPLETED
  > 
  > 07:28:21 /15.28.21 STC   59  IST270I  370X N12      NOW LOADED WITH LOADMOD N12
  > 07:28:21 /15.28.21 STC   59  IST093I  N10      ACTIVE
  > 07:28:21 /15.28.21 STC   59  IST093I  N10P3    ACTIVE
  > 07:28:21 /15.28.21 STC   59  IST093I  N11      ACTIVE
  > 
  > 07:28:26 /15.28.26 STC   59  IFL003I  IFLOADRN COMPLETED
  > 
  > 07:28:26 /15.28.26 STC   59  IST270I  370X N14      NOW LOADED WITH LOADMOD N14
  > 07:28:26 /15.28.26 STC   59  IST093I  N12      ACTIVE
  > 07:28:26 /15.28.26 STC   59  IST093I  N12P3    ACTIVE
  > 07:28:26 /15.28.26 STC   59  IST093I  N13      ACTIVE
  > 07:28:31 /15.28.31 STC   59  IST093I  N14      ACTIVE
  > 07:28:31 /15.28.31 STC   59  IST093I  N14P3    ACTIVE
  > 07:28:31 /15.28.31 STC   59  IST093I  N15      ACTIVE
  > 07:28:35 /15.28.34 STC   59  IST097I  VARY     ACCEPTED
  > 07:28:35 /15.28.34 STC   59  IST093I  T3767S11 ACTIVE
  > 07:28:35 /15.28.34 STC   59  IST097I  VARY     ACCEPTED
  > 07:28:35 /15.28.34 STC   59  IST093I  T3767S21 ACTIVE
  > 07:28:35 /15.28.34 STC   59  IST097I  VARY     ACCEPTED
  > 07:28:35 /15.28.34 STC   59  IST093I  T3767S31 ACTIVE
  > 07:28:35 /15.28.34 STC   59  IST097I  VARY     ACCEPTED
  > 07:28:35 /15.28.34 STC   59  IST093I  T3767S41 ACTIVE
  > 07:28:35 /15.28.34 STC   59  IST097I  VARY     ACCEPTED
  > 07:28:35 /15.28.34 STC   59  IST093I  T3278S11 ACTIVE
  > 07:28:35 /15.28.34 STC   59  IST097I  VARY     ACCEPTED
  > 07:28:35 /15.28.34 STC   59  IST093I  T3278S21 ACTIVE
  > 07:28:35 /15.28.34 STC   59  IST097I  VARY     ACCEPTED
  > 07:28:35 /15.28.34 STC   59  IST093I  T3278S31 ACTIVE
  > 07:28:35 /15.28.34 STC   59  IST097I  VARY     ACCEPTED
  > 07:28:35 /15.28.34 STC   59  IST093I  T3278S41 ACTIVE
  > 07:28:35 /15.28.34 STC   59  IST097I  VARY     ACCEPTED
  > 07:28:35 /15.28.34 STC   59  IST093I  T3278L11 ACTIVE
  > 07:28:35 /15.28.34 STC   59  IST097I  VARY     ACCEPTED
  > 07:28:35 /15.28.34 STC   59  IST093I  T3278L21 ACTIVE
  > 07:28:35 /15.28.34 STC   59  IST097I  VARY     ACCEPTED
  > 07:28:35 /15.28.34 STC   59  IST093I  T3767L31 ACTIVE
  > 07:28:35 /15.28.34 STC   59  IST097I  VARY     ACCEPTED
  > 07:28:35 /15.28.34 STC   59  IST093I  T3767L41 ACTIVE
  > 
  > 07:28:40 /15.28.40 STC   60  IED160I 3705 T07      LOAD=T07
  > 07:28:43 /15.28.43 STC   60  IED160I 3705 T10      LOAD=T10
  > 07:28:46 /15.28.46 STC   60  IED160I 3705 T12      LOAD=T12
  > 07:28:49 /15.28.49 STC   60  IED160I 3705 T14      LOAD=T14
  > 
  > 07:28:53 /15.28.52 STC   60  IED382I T07      ACTIVATE COMPLETE
  > 
  > 07:28:56 /15.28.55 STC   60  IED382I T10      ACTIVATE COMPLETE
  > 
  > 07:28:59 /15.28.58 STC   60  IED382I T12      ACTIVATE COMPLETE
  > 
  > 07:29:02 /15.29.01 STC   60  IED382I T14      ACTIVATE COMPLETE
  > 
  > 07:29:03 /15.29.03 STC   65  $HASP100 INISDSTD ON STCINRDR
  > 
  > 07:29:03 /15.29.03           MVS038J MVS 3.8j TK5 system initialization complete CN=00
  
  The string `MVS038J` was registered with HAO to trigger the execution of the script `scripts/tk5.rc`.
  
  ### Phase 2.2 -- ???
  
  ... and tk5.rc starts...
  
  > 07:29:03 HHC00081I Match at index 00, executing command script [scripts/tk5.rc](scripts/tk5.rc)
  > 07:29:03 HHC01603I script [scripts/tk5.rc](scripts/tk5.rc)
  > 07:29:03 HHC02260I Script 5: _begin processing_ file [scripts/tk5.rc](scripts/tk5.rc)
  > 07:29:03 HHC02262I Script 5: processing paused for 1000 milliseconds...
  
  > 07:29:03 /15.29.03 STC   65  $HASP373 INISDSTD STARTED
  > 07:29:03 /15.29.03 STC   65  IEF403I INISDSTD - STARTED - TIME=15.29.03
  > 07:29:03 /15.29.03 STC   50  +BSPRS99I - End of processing, MAXRC=0000
  > 07:29:03 /15.29.03 STC   65  IEF404I INISDSTD - ENDED - TIME=15.29.03
  > 07:29:03 /15.29.03 STC   65  $HASP395 INISDSTD ENDED
  > 07:29:03 /15.29.03 STC   65  $HASP150 INISDSTD ON PRINTER2        21 LINES
  > 07:29:03 /15.29.03           $HASP160 PRINTER2 INACTIVE - CLASS=Z
  > 07:29:03 /15.29.03 STC   65  $HASP250 INISDSTD IS PURGED
  > 
  > 07:29:04 HHC02263I Script 5: processing resumed...
  > 07:29:04 HHC01603I script [scripts/tk5_updates.rc](scripts/tk5_updates.rc)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file [scripts/tk5_updates.rc](scripts/tk5_updates.rc)
  > 07:29:04 HHC01603I script [scripts/tk5_updates/01](scripts/tk5_updates/01)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file [scripts/tk5_updates/01](scripts/tk5_updates/01)
  > 07:29:04 HHC02264I Script 5: file [scripts/tk5_updates/01](scripts/tk5_updates/01) _processing ended_
  > 07:29:04 HHC01603I script [scripts/tk5_updates/02](scripts/tk5_updates/02)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file scripts/tk5_updates/02
  > 07:29:04 HHC02264I Script 5: file [scripts/tk5_updates/02](scripts/tk5_updates/02) _processing ended_
  > 07:29:04 HHC01603I script [scripts/tk5_updates/03](scripts/tk5_updates/03)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file scripts/tk5_updates/03
  > 07:29:04 HHC02264I Script 5: file [scripts/tk5_updates/03](scripts/tk5_updates/03) _processing ended_
  > 07:29:04 HHC01603I script [scripts/tk5_updates/04](scripts/tk5_updates/04)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file scripts/tk5_updates/04
  > 07:29:04 HHC02264I Script 5: file [scripts/tk5_updates/04](scripts/tk5_updates/04) _processing ended_
  > 07:29:04 HHC01603I script [scripts/tk5_updates/05](scripts/tk5_updates/05)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file scripts/tk5_updates/05
  > 07:29:04 HHC02264I Script 5: file [scripts/tk5_updates/05](scripts/tk5_updates/05) _processing ended_
  > 07:29:04 HHC01603I script [scripts/tk5_updates/06](scripts/tk5_updates/06)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file scripts/tk5_updates/06
  > 07:29:04 HHC02264I Script 5: file [scripts/tk5_updates/06](scripts/tk5_updates/06) _processing ended_
  > 07:29:04 HHC01603I script [scripts/tk5_updates/07](scripts/tk5_updates/07)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file scripts/tk5_updates/07
  > 07:29:04 HHC02264I Script 5: file [scripts/tk5_updates/07](scripts/tk5_updates/07) _processing ended_
  > 07:29:04 HHC01603I script [scripts/tk5_updates/08](scripts/tk5_updates/08)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file scripts/tk5_updates/08
  > 07:29:04 HHC02264I Script 5: file [scripts/tk5_updates/08](scripts/tk5_updates/08) _processing ended_
  > 07:29:04 HHC01603I script [scripts/tk5_updates/09](scripts/tk5_updates/09)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file scripts/tk5_updates/09
  > 07:29:04 HHC02264I Script 5: file [scripts/tk5_updates/09](scripts/tk5_updates/09) _processing ended_
  > 07:29:04 HHC01603I script [scripts/tk5_updates/10](scripts/tk5_updates/10)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file [scripts/tk5_updates/10](scripts/tk5_updates/10)
  > 07:29:04 HHC02264I Script 5: file [scripts/tk5_updates/10](scripts/tk5_updates/10) _processing ended_
  > 07:29:04 HHC02264I Script 5: file [scripts/tk5_updates.rc](scripts/tk5_updates.rc) _processing ended_
  > 
  > 07:29:04 HHC01603I script [scripts/local.rc](scripts/local.rc)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file [scripts/local.rc](scripts/local.rc)
  > 07:29:04 HHC01603I script [local_scripts/01](local_scripts/01)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file local_scripts/01
  > 07:29:04 HHC02264I Script 5: file [local_scripts/01](local_scripts/01) _processing ended_
  > 07:29:04 HHC01603I script [local_scripts/02](local_scripts/02)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file [local_scripts/02](local_scripts/02)
  > 07:29:04 HHC02264I Script 5: file [local_scripts/02](local_scripts/02) _processing ended_
  > 07:29:04 HHC01603I script [local_scripts/03](local_scripts/03)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file [local_scripts/03](local_scripts/03)
  > 07:29:04 HHC02264I Script 5: file [local_scripts/03](local_scripts/03) _processing ended_
  > 07:29:04 HHC01603I script [local_scripts/04](local_scripts/04)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file [local_scripts/04](local_scripts/04)
  > 07:29:04 HHC02264I Script 5: file [local_scripts/04](local_scripts/04) _processing ended_
  > 07:29:04 HHC01603I script [local_scripts/05](local_scripts/05)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file local_scripts/05
  > 07:29:04 HHC02264I Script 5: file [local_scripts/05](local_scripts/05) _processing ended_
  > 07:29:04 HHC01603I script [local_scripts/06](local_scripts/06)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file [local_scripts/06](local_scripts/06)
  > 07:29:04 HHC02264I Script 5: file [local_scripts/06](local_scripts/06) _processing ended_
  > 07:29:04 HHC01603I script [local_scripts/07](local_scripts/07)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file [local_scripts/07](local_scripts/07)
  > 07:29:04 HHC02264I Script 5: file [local_scripts/07](local_scripts/07) _processing ended_
  > 07:29:04 HHC01603I script [local_scripts/08](local_scripts/08)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file [local_scripts/08](local_scripts/08)
  > 07:29:04 HHC02264I Script 5: file [local_scripts/08](local_scripts/08) _processing ended_
  > 07:29:04 HHC01603I script [local_scripts/09](local_scripts/09)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file [local_scripts/09](local_scripts/09)
  > 07:29:04 HHC02264I Script 5: file [local_scripts/09](local_scripts/09) _processing ended_
  > 07:29:04 HHC01603I script [local_scripts/10](local_scripts/10)
  > 
  > 07:29:04 HHC02260I Script 5: _begin processing_ file [local_scripts/10](local_scripts/10)
  > 07:29:04 HHC02264I Script 5: file [local_scripts/10](local_scripts/10) _processing ended_
  > 07:29:04 HHC02264I Script 5: file [scripts/local.rc](scripts/local.rc) _processing ended_
  > 
  > 07:29:04 HHC02262I Script 5: processing paused for 1000 milliseconds...
  > 07:29:05 HHC02263I Script 5: processing resumed...
  > 07:29:05 HHC01603I *
  > 07:29:05 HHC01603I *                           TTTTTTTTTTTT   KKKK  KKKKK     555555555555
  > 07:29:05 HHC01603I *                           TT   TT   TT    KK    KK       55
  > 07:29:05 HHC01603I *                           TT   TT   TT    KK   KK        55      Update 4
  > 07:29:05 HHC01603I *                                TT         KK  KK         55
  > 07:29:05 HHC01603I *        4l      _,,,---,,_      TT         KK KK          55
  > 07:29:05 HHC01603I * ZZZzz /,'.-'`'    -.  ;-;;,    TT         KKKK           55555555555
  > 07:29:05 HHC01603I *      4,4-  ) )-,_. ,( (  ''-'  TT         KKKKK                    55
  > 07:29:05 HHC01603I *     '---''(_/--'  `-')_)       TT         KK  KK                   55
  > 07:29:05 HHC01603I *                                TT         KK   KK                  55
  > 07:29:05 HHC01603I *       The MVS 3.8j             TT         KK    KK                 55
  > 07:29:05 HHC01603I *     Tur(n)key System           TT         KK     KK                55
  > 07:29:05 HHC01603I *                              TTTTTT      KKKK     KKK    55555555555
  > 07:29:05 HHC01603I *
  > 07:29:05 HHC01603I *     TK3 created by Volker Bandke       volker@bandke.org
  > 07:29:05 HHC01603I *     TK4- update by Juergen Winkelmann  juergen.winkelmann@pebble-beach.ch
  > 07:29:05 HHC01603I *     TK5  update by Rob Prins           prin0096@gmail.com
  > 07:29:05 HHC01603I *          see SYS2.JCLLIB(CREDITS) for complete credits
  > 07:29:05 HHC01603I *
  > 07:29:05 HHC02264I Script 5: file [scripts/tk5.rc](scripts/tk5.rc) _processing ended_
  
  
  ```