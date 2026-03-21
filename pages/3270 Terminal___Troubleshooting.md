-
- ## Host write error
	- Depending on your terminal configuration, you can get an error like this...
	- ```
	  Host write error:
	  RA address 2081 > maximum 1919
	  ```
	- This basically means that the host is trying to write on a part of the screen that's outside the bounds of your terminal session.
	- Fix:
		- (temporarily) select a larger model
			- (e.g. 3278-5) — model 5 supports 27x132
			-