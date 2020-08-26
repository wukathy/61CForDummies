# RISC-V

## Registers vs Memory
**Registers:** on-chip memory, store 32-bit values, allow for fast access— **only** 32 general purpose registers. 
For main memory use `sw` and `lw`.

## Special Registers
- **Program Counter:** special purpose register
    - Store the address of current instruction – load actual instruction in from IMEM at
    beginning of cycle
    - PC + 4 [word size per RISC-V version]
    - Generally, jump instructions will have `ra` as the destination register, setting the return
    address of a function to the current PC + 4
- **Stack Pointer:** general purpose register
    - Points to bottom of stack
    - Manage information of current function call

## Full Memory Layout
- `PC` points to code
- `SP` points to bottom of stack
- `GP` points to top of heap (only used in compilers)
- Programmer can use other registers to point to data structures contained in static data and heap  

{{< hint warning >}}
**Calling Convention**  
Registers guaranteed to be saved across a function call: saved registers (`s**`), `sp`. Distinguish caller/callee saved registers.
{{< /hint >}}

## Instruction Formats
- _R-type:_ register-register arithmetic operations
- _I-type:_ register-immediate arithmetic operations and memory loads and jalr
- _S-type:_ memory stores
- _B-type:_ branch instructions
- _U-type:_ upper immediate instructions
- _J-type:_ jal (not jalr) 

Immediates are right-indexed.  
*insert explanation for how to convert RISC-V instruction to machine code*  
Size of a word: 4 bytes

## J Instructions
{{< tabs "instructions" >}}
{{< tab "jal" >}}
**jal is Jump-And-Link (`jal rd offset`)**.  
This instruction stores PC+4 into the register destination and jumps to a certain offset from the given PC . 
This is used when you only know the offset of where you want to go and also want to remember where you are.
1. jal can also be used with a label instead of an offset. Using `jal ra Square`, this will STORE PC+4 into ra and jump to the Square label. This is technically a pseudo-instruction.
2. If there is no specified rd (i.e. `jal Label`), then pretend there is an implicit register “ra”. It acts as if it’s also a pseudo-instruction. So (`jal Square`) is really `jal ra Square`.  

**Example**: `jal ra 20` will store PC+4 into ra and jump to PC+20.
{{< /tab >}}

{{< tab "jalr" >}}
**jalr is Jump-And-Link-Register (`jalr rd rs1 offset`)**.  
This instruction jumps to the specific address stored in rs1 + offset, and stores PC+4 into rd. This is used when we have the address of the location we want to go to (which might include an offset) and want to remember where we are now.

**Example**: `jalr ra rs1 0` will store PC+4 into register ra and jump to where rs1 is, plus offset of 0. Jumping means PC will also be set to that location.
{{< /tab >}}

{{< tab "j" >}}
**j is Jump (`j Label`)**.  
This is a pseudo-instruction for jal that jumped to a certain label without storing where PC+4 is. We want to use j when we only have the label of where to go, and don't want to remember where we are. Key point: `j Label` is _the same as_ `jal x0 Label`.

**Example**: `j Loop` will jump PC to where Loop is located. That's it! It implicitly stores PC+4 into x0, but this actually does nothing since editing x0 does nothing. 

{{< /tab >}}

{{< tab "jr" >}}
**jr is Jump-Register (`jr rs1`)**.  
This is also a pseudo-instruction for jalr. It will jump to a certain address stored in rs1 with no offset, and it doesn't store PC+4 into anywhere. Key point: `jr rs1` _is the same as_ `jalr x0 rs1 0`. We want to use jr when we want to jump to a memory address stored in a register (and no offset) and we don't want to remember where we are.

**Example**:`jr ra`. We store PC+4 into x0, which does nothing because x0 can't be edited. This instruction jumps to the location that ra contains with NO offset. 
{{< /tab >}}
{{< /tabs >}}

