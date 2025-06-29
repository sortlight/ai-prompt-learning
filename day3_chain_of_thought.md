#  Day 3: Chain-of-Thought (CoT) Prompting Step by Step Reasoning

Today’s focus was **Chain of Thought prompting** which guides the AI to reason step by step instead of jumping to conclusions. This is super helpful when analyzing smart contract logic, debugging and explaining attacker flow.

---

##  Prompt 1: Solidity Debugging — CoT Style

**Prompt:**  
You are a Solidity tutor. I will paste a function, and I want you to walk through the logic line by line. If there are issues, explain how they could cause errors or vulnerabilities. Think step-by-step and reason like you're explaining to a junior dev.



**Code Example:**
```solidity
function buyTokens() public payable {
    require(msg.value >= 1 ether, "Minimum 1 ETH");

    uint tokensToBuy = msg.value / tokenPrice;
    require(tokensToBuy > 0, "Not enough ETH");

    balances[msg.sender] += tokensToBuy;
    totalTokensSold += tokensToBuy;

    payable(owner).transfer(msg.value);
}

```
Expected AI Output:

Check: Buyer must send at least 1 ETH.

Divides ETH sent by tokenPrice to calculate how many tokens to give.

If tokenPrice == 0, this causes a division by zero error.

No check if contract has enough tokens to sell.

Could fail if owner is a contract that rejects Ether.

Improvement: Add check for contract token balance before updating balances.



## Prompt 2: Model an Attacker's Logic (Security Mindset)

**Prompt**:
You are a black-hat hacker reviewing this smart contract. I want you to think step-by-step like a real attacker would. Explain how you'd approach breaking or exploiting the function.

**Code Example:**
```solidity
mapping(address => uint256) public deposits;

function refund() public {
    uint amount = deposits[msg.sender];
    require(amount > 0, "No funds");

    (bool sent, ) = msg.sender.call{value: amount}("");
    require(sent, "Failed");

    deposits[msg.sender] = 0;
}

```
Expected AI Output:

Step 1: See if attacker has funds in deposits.

Step 2: Notice the use of call — allows for fallback execution.

Step 3: If attacker is a contract, fallback can reenter refund() before balance is reset.

Step 4: Drain funds through reentrancy.

Fix: Apply Checks-Effects-Interactions pattern. Update balance before transfer.




