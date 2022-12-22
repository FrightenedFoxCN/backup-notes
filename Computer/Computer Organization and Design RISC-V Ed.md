

# Computer Organization and Design RISC-V Ed.

## Computer Abstractions and Technology

## Instructions: Language of the computer(RISC-V Ed.)

|             Instruction              |       Example       |           Meaning            |                          Comments                          |
| :----------------------------------: | :-----------------: | :--------------------------: | :--------------------------------------------------------: |
|            **Arithmetic**            |                     |                              |                                                            |
|                 Add                  |  `add x5, x6, x7`   |         x5 = x6 + x7         |                  Three register operands                   |
|               Subtract               |  `sub x5, x6, x7`   |         x5 = x6 - x7         |                  Three register operands                   |
|            Add immediate             |  `addi x5, x6, 20`  |         x5 = x6 + 20         |                      Adding constants                      |
|          **Data Transfer**           |                     |                              |                                                            |
|           Load doubleword            |   `ld x5, 40(x6)`   |     x5 = Memory[x6 + 40]     |                 DW from memory to register                 |
|           Store doubleword           |   `sd x5, 40(x6)`   |     Memory[x6 + 40] = x5     |                 DW from register to memory                 |
|              Load word               |   `lw x5, 40(x6)`   |     x5 = Memory[x6 + 40]     |                 W from memory to register                  |
|              Store word              |   `sw x5, 40(x6)`   |     Memory[x6 + 40] = x5     |                 W from register to memory                  |
|         Load word, unsigned          |  `lwu x5, 40(x6)`   |     x5 = Memory[x6 + 40]     |                 UW from memory to register                 |
|         Store word, unsigned         |  `swu x5, 40(x6)`   |     Memory[x6 + 40] = x5     |                 UW from register to memory                 |
|            Load halfword             |   `lh x5, 40(x6)`   |     x5 = Memory[x6 + 40]     |                 HW from memory to register                 |
|            Store halfword            |   `sh x5, 40(x6)`   |     Memory[x6 + 40] = x5     |                 HW from register to memory                 |
|              Load byte               |   `lb x5, 40(x6)`   |     x5 = Memory[x6 + 40]     |                Byte from memory to register                |
|              Store byte              |   `sb x5, 40(x6)`   |     Memory[x6 + 40] = x5     |                Byte from register to memory                |
|            Load reserved             |   `lr.d x5, (x6)`   |       x5 = Memory[x6]        |               Load, 1st half of atomic swap                |
|          Store conditional           | `sc.d x7, x5, (x6)` | Memory[x6] = x5 : x7 = 0 / 1 |               Store, 2nd half of atomic swap               |
|         Load upper immediate         |  `lui x5, 0x12345`  |       x5 = 0x12345000        |                                                            |
|             **Logical**              |                     |                              |                                                            |
|                 And                  |  `and x5, x6, x7`   |         x5 = x6 & x7         |          Three register operands, bit-by-bit AND           |
|             Inclusive or             |   `or x5, x6, x8`   |        x5 = x6 \| x8         |           Three register operands, bit-by-bit OR           |
|             Exclusive or             |  `xor x5, x6, x9`   |         x5 = x6 ^ x9         |          Three register operands, bit-by-bit XOR           |
|            And immediate             |  `andi x5, x6, 20`  |         x5 = x6 & 20         |           Bit-by-bit AND register with constant            |
|        Inclusive or immediate        |  `ori x5, x6, 20`   |        x5 = x6 \| 20         |            Bit-by-bit OR register with constant            |
|        Exclusive or immediate        |  `xori x5, x6, 20`  |         x5 = x6 ^ 20         |           Bit-by-bit XOR register with constant            |
|              **Shift**               |                     |                              |                                                            |
|          Shift left logical          |  `sll x5, x6, x7`   |        x5 = x6 << x7         |                   Shift left by register                   |
|         Shift right logical          |  `srl x5, x6, x7`   |        x5 = x6 >> x7         |                  Shift right by register                   |
|        Shift right arithmetic        |  `sra x5, x6, x7`   |        x5 = x6 >> x7         |             Arithmetic shift right by register             |
|     Shift left logical immediate     |  `slli x5, x6, 3`   |         x5 = x6 << 3         |                  Shift left by immediate                   |
|    Shift right logical immediate     |  `srli x5, x6, 3`   |         x5 = x6 >> 3         |                  Shift right by immediate                  |
|   Shift right arithmetic immediate   |  `srai x5, x6, 3`   |         x5 = x6 >> 3         |            Arithmetic shift right by immediate             |
|        **Conditional Branch**        |                     |                              |                                                            |
|           Branch if equal            |  `beq x5, x6, 100`  |  if(x5 == x6) goto PC + 100  |           PC-relative branch if registers equal            |
|         Branch if not equal          |  `bne x5, x6, 100`  |  if(x5 != x6) goto PC + 100  |         PC-relative branch if registers not equal          |
|         Branch if less than          |  `blt x5, x6, 100`  |  if (x5 < x6) goto PC + 100  |            PC-relative branch if registers less            |
|      Branch if greater or equal      |  `bge x5, x6, 100`  | if (x5 >= x6) goto PC + 100  |      PC-relative branch if registers greater or equal      |
|    Branch if less than, unsigned     | `bltu x5, x6, 100`  |  if (x5 < x6) goto PC + 100  |       PC-relative branch if registers less, unsigned       |
| Branch if greater or equal, unsigned | `bgeu x5, x6, 100`  |  if(x5 >= x6) goto PC + 100  | PC-relative branch if registers greater or equal, unsigned |
|       **Unconditional branch**       |                     |                              |                                                            |
|            Jump and link             |    `jal x1, 100`    |  x1 = PC + 4; goto PC + 100  |                 PC-relative procedure call                 |
|        Jump and link register        | `jalr x1, 100, x5`  |  x1 = PC + 4; goto x5 + 100  |              Procedure return; indirect call               |

