---
layout: post
title: "Tron - How to talk to a smart contract"
preview: "Yield farming website is down? Panic is activating? Check this quick and simple guide..."
image: /assets/images/unsplashed/farming.jpg
date: 2020-09-10 15:50:31 +0300
categories: crypto
---
# Yield farming website is down? Panic is activating? Check this quick and simple guide to bypass the website and interact directly with Tron smart contracts.

1. Go to the [tronscan](https://tronscan.org/) website.
2. Find the smart contract you want to interact with. Best way is to search for your earlier transaction when you interacted with it.
3. On tronscan's smart contract address go to the contract tab. Here you will have 3 subtabs (Code, Read Contract and Write Contract).
4. Check the `Contract codes` solidity code. This step is to validate that the function you want to  call (e.g. `exit()`) does want you want it to do. On Tron, the contract can be closed source, meaning that you cannot see the source code files. If you interact with a smart contract without open source code you put all your trust into the person behind it. I recommend to not use any contract that isn't open source.
  - a yield farming `exit()` function example from [dragonfi](https://tronscan.org/#/contract/TWJGyUGgYb283CWchS4o8iBnH8xWSdFH81/code)
  ```javascript
    function exit() external {
        withdraw(balanceOf(msg.sender));
        getReward();
    }
  ```
  - the `exit` function calls other 2 methods
  ```javascript
    function withdraw(uint256 amount) public {
        _totalSupply = _totalSupply.sub(amount);
        _balances[msg.sender] = _balances[msg.sender].sub(amount);
        y.safeTransfer(msg.sender, amount);
    }
    function getReward() public updateReward(msg.sender) checkhalve checkStart{
        uint256 reward = earned(msg.sender);
        if (reward > 0) {
            rewards[msg.sender] = 0;
            dragon.safeTransfer(msg.sender, reward);
            emit RewardPaid(msg.sender, reward);
        }
    }
  ```
  - if you cannot validate the code, use only audited contracts
5. Then go to the `Write Contract` tab and press `Send` button under the function's name. It will ask you to connect to your Tronlink wallet to be able to sign the transaction.

# Safe Farming! 
Tron address: THBW6zVALYiRFi4w8GqD4wFaokZxerV4KT