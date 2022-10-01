fvictorio/evm-puzzles
=======

Puzzle 1 
-----------
An easy one, we're doing the jump to the number which came as a call parameter

Puzzle 2 
-----------
Codesize is total instructions + 1
SUB is subtraction
So Codesize minus the value sent should equal to JUMPDEST, which is 6

Puzzle 3 
-----------
Calldatasize in bytes - we just need to send 4 bytes

Puzzle 4 
-----------
XOR calculation will do CODESIZE ^ CALLVALUE(which is the argument we send) and it should be 0A(10dec)
So it's 12 ^ CALLVALUE = 10 or 12^10=CALLVALUE which is 6

Puzzle 5 
-----------
CALLDATA squared is compared to 0100, JUMPI is performed if the comparison is true.
0100 are 256 dec, sqrt is 16

Puzzle 6 
-----------
We are using calldata as JUMPDEST, it should be 0a, but padded:
32 bytes 0x000...000a

Puzzle 7 
-----------
CREATE deploys a contract and it's bytcode size next is compared to 1 for equality.
CREATE takes 3 parameters from stack (val of wei, offset of bytecode location(deployment), and length of that bytecode)
00      6001      PUSH1 01        [01]
01      6000      PUSH1 00        [00, 01] (offset, size)
02      F3        RETURN          []
Which is 0x60016000F3 concatenated

Puzzle 8 
-----------
Deploying with CREATE, just like previous.
Then calling the previously deployed contract. And we need the call to return 00, which means to fail or REVERT.
00      60FD      PUSH1 FD        [FD]
01      6000      PUSH1 00        [00, FD] (offset, value)
02      53        MSTORE8         [] // Wrote REVERT to memory
03      6001      PUSH1 01        [01]
04      6000      PUSH1 00        [00, 01] (offset, size)
05      F3        RETURN          [] // Returns REVERT from memory
0x60FD60005360016000F3

Puzzle 9 
-----------
Length of the calldata must be > 3
Then we multiply it by value and should get 8
So 4 bytes of calldata and 2 as value

Puzzle 10
-----------
if (CODESIZE > CALLVALUE) {
  jumpTo(0x08)
}

if (CALLDATASIZE % 3 == 0) {
  jumpTo(0x0a + CALLVALUE)
}


value is 15
calldata - just 3 bytes
