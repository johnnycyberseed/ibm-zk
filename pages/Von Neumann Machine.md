- The conceptual framework used by most computers.
- Devised by [[John von Neumann]]
-
- {{renderer :mermaid_683d094f-5050-4365-b0df-222f2fecec64, 2}}
  collapsed:: true
	- ```mermaid
	  graph TD;
	    control[Control Unit]
	    ins[Input Units]
	    mem[Memory]
	    alu[Arithmetic and Logic Unit]
	    outs[Output Units]
	    
	    control <-.-> ins
	    control <-.-> mem
	    control <-.-> outs
	    ins <==> alu
	    outs <==> alu
	    mem <-.-> alu
	  
	  ```
	-
- Dashed lines : Control
- Solid lines: Data
- ### Arithmetic and Logic Unit
	- Does math: add, subtract, multiply, divide
	- Does logic ops: shift, conjunction, disjunction, complementation.
	- reads/writes to memory
- ### Memory
	- a linear array of cells numbered from 1 to _n_
	- use to store both data and program (known as a [[stored program]])
- ## Core Characteristics
	- data and instructions are stored in memory
		- which means programs can be modified _during_ execution
		- no distinction is made between data types (e.g. decimal vs. binary vs. floating point vs. character string)
	- programs are stored in memory and execute sequentially (the [[program counter]] points to the next instruction in memory)
	- data flows only from/to "Input Units"/"Output Units" into the ALU; not directly into memory
	- the control unit fetches, decodes, and executes each instruction in sequence.
	-
-
	-
	-