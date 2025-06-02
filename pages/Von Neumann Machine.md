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
- ## Arithmetic and Logic Unit
	- Does math: add, subtract, multiply, divide
	- Does logic ops: shift, conjunction, disjunction, complementation.
- ## Memory
	- a linear array of cells numbered from 1 to _n_
	- use to store both data and program (known as a [[stored program]])
- ## Data Flow
	- Data flows only from/to Output Units/Input
	-