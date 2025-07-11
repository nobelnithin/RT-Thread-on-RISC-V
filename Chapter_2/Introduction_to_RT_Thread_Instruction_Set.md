# Introduction to RISC V Instruction Set

The RISC-V instruction set was introduced in 2010 by Professor Krste Asanovic(opens in a new tab) at the University of California, Berkeley, along with contributors like Yunsup Lee(opens in a new tab). It is characterized as a compact 
instruction set architecture.

Instruction set are categorized into two types: **Complex** instruction sets and **Compact** instruction sets. Complex Instruction sets allows single instruction to perform intricate tasks, while compact instruction sets break complex
task into multiple instructions.  Although complex instruction sets may simplify CPU design and reduce code complexity, they can also lead to increased design complexity. Conversely, compact instruction sets may require more instructions to achieve the same functionality, potentially increasing both code size and complexity. Nonetheless, the prevailing trend in development leans towards simpler instruction sets.

A distinguishing feature of the RISC-V instruction set is its modularity. The RV32I instruction set is essential for implementing a complete software stack. CPU designers have the flexibility to select specific instruction modules based on their actual requirements, allowing for customized implementations tailored to various applications.

### Instruction Format

RISC-V has six basic instruction formats: R, I, S, B, U, J.

1) R-Type Instructions: Used for Register-to-Register arithmetic operations.

2) I-Type Instructions: Used for Register-to-Register arithmetic operations and read/load memory operations.

3) S-Type Instructions: For write/store in memory.

4) B-Type Instructions: For conditional jump operations.

5) U-type Instructions: For high 20-bit immediate number (long immediate number) operations.

6) J-Type Instructions: For unconditional jump operations.

There are only six formats of RISC-V instructions, and their instruction formats have the following characteristics:

1) All Instructions are 32-bits in length, first 7 bits are opcode, which is a sigle instruction that executed by CPU

2) The identifiers for reading and writing registers are in the same location, so the registers can be accessed before decoding the instruction.
  
3) The immediate numeric segment is a sign extension, and the sign bit is kept in the highest bit.

#### The composition of 6 Instruction Structures
<img width="970" height="354" alt="image" src="https://github.com/user-attachments/assets/5f201005-9561-4a6f-a8b4-3738529a9625" />

Opcode: This is a single instruction, which represent type of instruction.

rd: Distination Operation Register. This field holds the encoding of the destination register, which is used to hold the result of the operation.

funct3: Function code field. This field occupies 3bits.

rs1: First Source operand register.

rs2: Second Source operand register.

funct7: Function Code Field. This occupies 7bits.

imm: Immediate digital field

