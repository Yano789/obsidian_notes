used to create a [[Process]]
## Purpose of Fork (Shell POV)
1. Create a new [[Process]]
2. Exec binary to that new [[Process]]
3. Shell can prompt new command when child [[Process]] terminates (not replaced)

Creates a [[Binary Tree]] based on depth/how many times the fork() [[Function]] is called
- to get the number of [[Process|processes]] at the end: 
	- $2^n$ 
	- where n is the depth of the [[Tree Graph|tree]] 