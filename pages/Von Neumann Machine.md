- The conceptual framework used by most computers.
- Devised by [[John von Neumann]]
-
- {{renderer :mermaid_683d094f-5050-4365-b0df-222f2fecec64, 2}}
	- ```mermaid
	  graph TD;
	    control[Control Unit]
	    ins[Input Units]
	    mem[Memory]
	    aru[Arithmetic and Logic Unit]
	    outs[Output Units]
	    
	    control <-.-> ins
	    control <-.-> mem
	    control <-.-> outs
	    ins <==> aru
	    outs <==> aru
	    mem <-.-> aru
	  
	  ```
	-
- Dashed lines : Control
- Solid lines: Data
-