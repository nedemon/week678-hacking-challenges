Ethernaut
=======

Ethernaut 3 (insecure randomness)
-----------
Attacker contract supposed to use the same block - then the guess will always be correct.
The challenge contract is too tied to previous blockhash.

Ethernaut 4 (solidity understanding)
-----------
This challenge is all about difference between tx.origin and msg.sender

Ethernaut 5 (arithmetic overflow/underflow)
-----------
Since we are dealing with uints, underflow checks for negative numbers won't work.

Ethernaut 10 (Re-entrancy)
-----------
Internal state is only updates after the transfer is done so receive function would help us  
to drain the contract.

Ethernaut 11 (understanding interfaces)
-----------
If victim is using an interface to check some condition, it's a good place to put any logic there.
Even that which serves our purposes.

Ethernaut 15 (understanding ERC20 protocol)
-----------
In ERC20 token there are 2 different methods for transferring tokens.
One is just transfer and another one is transfer after approval.
Unless you're hiding the second one, changing just a single one doesn't make sense.

Ethernaut 17 (solidity understanding)
-----------
Selfdestruct out of destroy method offers a really neat way to drain the contract.

Ethernaut 20 (solidity understanding)
-----------
Once you set the partner contract and write the fallback function with an infinite loop,
it's gonna consume all the funds of the victim contract.

Ethernaut 21 (understanding interfaces)
-----------
Similar to Elevator, we are in charge of an interface which returns isSold.
That var could be used to distinguish first or second call to the contract.

Capture the ether
=======

Guess the Number (warmup challenge)
-----------
The number is hardcoded, nothing interesting here.

Guess the random number (insecure randomness)
-----------
Brute-forcing all the uint8 values until the hash matches - a fairly easy task, just compute intensive.

Guess the secret number (solidity understanding)
-----------
It's as simple as querying the storage slot 0 - and converting to decimal.

Guess the new number (insecure randomness)
-----------
All the steps could be emulated inside attacker contract and then ether is just takes from the victim.


Predict the future (solidity understanding)
-----------
Spamming transaction would work and we will hit the result eventually because it is in [0,9] range.

Predict the block hash (solidity understanding)
-----------
After 256 blocks blockhash returns 0 result, so we need to commit the guess and wait.

Token bank (re-entrancy, understanding token protocols)
-----------
Attacker contract is given an allowance and withdraws 500k tokens.
Which could be used to trigger a reentrancy attack to drain the balance.

Token sale (arithmetic overflow/underflow)
-----------
If numTokens is 2^256 / 10^18 we can force an overflow in the check.

Token whale (arithmetic overflow/underflow)
-----------
msg.sender could help us underflow the balance and get all the tokens


Damn Vulnerable Defi
=======
1 Unstoppable (faulty business logic)
-----------
Pool balance is never updates since tokens got into the contract through transfer and not through depositTokens.
As a result, assert condition fails.

2 Naive Receiver (solidity understanding)
-----------
receiveEther - no checks for initiator of loan.
flashLoan - no checks for borrowAmount == 0  
for (let i = 0; i < 10; i++) {  
await this.pool.connect(attacker).flashLoan(this.receiver.address, "0")  
}

3 Truster (understanding imported libraries)
-----------
This is really unsafe - target.functionCall(data); - just calling some data  


4 Side Entrance (faulty business logic)
-----------
execute function call on an interface from msg.sender is a suspicious implementation

