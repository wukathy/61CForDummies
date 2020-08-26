# CALL

All of CALL are programs!
- **Compiler** (.c -> .s)
	- May contain pseudoinstructions, from high level programming language to lower level.
- **Assembler** (.s → .o)
	- Create machine language from lower level
	- Replaces pseudo instructions
	- Two passes:
		1. Replace pseudo instructions
		2. Generate relative obj
	- Set up info for linker
	- Creates symbol table: keeps track of labels and data for _other_ files
	- Relocation table: keeps track of addresses from other files that are used by _this_ file
- **Linker** (.o -> executable, a.out [default])
	- Link file texts, data, relocate necessary addresses
	- Update and fill in absolute addresses that Assembler looked at
- **Loader** (executable -> run!)
	- Load executables into memory and run
	- Create new address space
	- Copies instructions
	- Copies args in program to stack
	- Initialize machine registers

![CALL](/images/call.png)
