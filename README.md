# Solidity Resources

This compilation is intended to relay facts about Solidity in a somewhat comprehensive manner, without providing much explanation.  This is a starting point and ongoing reference for Solidity developers and should contain many, but not all, important facts about Solidity.  A goal in compiling this has been to condense facts that can be taken away from documentation.  If a sentence in official documentation implies something but doesn't come out and specifically say something we have tried to condense those sentences into _actionable_ items here.  Many actionable items that are spelled out as such in the original source (for instance the "!Note" and "!Warning" [here](http://idorecall.com/blog/about/)) are not repeated here though this file may repeat some of the more important items. 

Solidity as a language is rapidly changing, so please feel free to submit updates as PRs!  Please link to the source, as that is the best way for us to verify facts and learn more.



## Security Best Practices

- To prevent replay attacks whereby an attacker is able to repeatedly call a function beneficial to them, set the balance of their account to 0 or the reduced number _prior_ to sending them ether
        
        
        function withdrawRefund() external {
          uint refund = refunds[msg.sender];
          refunds[msg.sender] = 0; // <- user's balance set to 0 prior to sending to prevent being able to "replay" `.send()` on following line
          if (!msg.sender.send(refund)) {
            refunds[msg.sender] = refund; // reverting state because send failed
          }
        }

## Abstract Contracts

- [Main DOCS](http://solidity.readthedocs.io/en/develop/contracts.html#abstract-contracts)
- 


## Contract Constructor Functions

- Constructor functions are functions that have the same name as the contract
- Constructor functions are optional
- Only one constructor function is allowed which means overloading is not supported


## Modifiers

- `internal` - infamous for the multi-sig wallet hack on 19/7/2017, this function modifier means that the function can only be called within the contract itself.
- `payable` - functions must use this keyword to receive ether


## General

 - If you use `var` you will get a compiler warning.  You shouldn't use `var`.  It will use the `uint8` type.  This will be disallowed in future versions of Solidity.

## Interfaces

- [Main Docs](http://solidity.readthedocs.io/en/develop/contracts.html#interfaces)

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
- [ ] Is all data inside your contract whether at deploy time or after being called by any user intended to be public?


## Links + Sources



