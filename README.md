# Solidity Resources

This compilation is intended to relay facts about Solidity in a somewhat comprehensive manner, without providing much explanation.  It is intended to be a starting point for beginning Solidity developers and should contain many, but not all, important facts about Solidity.  Also, the language is rapidly changing, so please feel free to submit updates as PRs!

## Security Best Practices

- To prevent replay attacks wherebuy an attacker is able to repeatedly call a function beneficial to them, set the balance of their account to 0 or the reduced number _prior_ to sending them ether.
  - 

## Math

- Integer division rounds down, so avoid it until the fixed-point type is implemented or use a multiplier ([link](https://github.com/ConsenSys/smart-contract-best-practices#beware-rounding-with-integer-division))


## Fallback functions

- The only unnamed functions allowed in contracts ([link](http://solidity.readthedocs.io/en/latest/contracts.html#fallback-function))
- They cannot have arguments and cannot return anything ([link](http://solidity.readthedocs.io/en/latest/contracts.html#fallback-function))
- If you want to send ether to a contract it must contain a `payable` fallback function or else the contract will throw an exception
  - `"Sending Ether to this contract will cause an exception, because the fallback function does not have the "payable"`([link](http://solidity.readthedocs.io/en/develop/contracts.html#fallback-function))
- Fallback functions receive a gas stipend of 2300 gas which greatly limits what they can do ([link](http://solidity.readthedocs.io/en/latest/contracts.html#fallback-function))


## Solidity Contract Checklist

- [ ] Do I reset the senders balance before sending them to prevent DAO-type attacks? 
- [ ] If the contract is supposed to receive ether (and keep them) does my fallback function have the `payable` keyord?
- [ ] If using a loop that is expected to possibly loop more than 255 times, have I declared the iterator variable in the loop as some integer type larger than `uint8`?
- [ ] If I use integer divions am I using a multiplier to prevent Solidity from rounding down?
- [ ] 


## Links + Sources



