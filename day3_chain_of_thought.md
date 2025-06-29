#  Day 3: Chain-of-Thought (CoT) Prompting Step by Step Reasoning

Today’s focus was **Chain of Thought prompting** which guides the AI to reason step by step instead of jumping to conclusions. This is super helpful when analyzing smart contract logic, debugging and explaining attacker flow.

---

##  Prompt 1: Solidity Debugging _____ CoT Style

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


## Prompt 3: Explain Gas Optimization 
**Prompt:** 
I will paste a Solidity function. I want you to walk through each line and explain whether it is gas efficient or not. Think step-by-step and suggest improvements with reasoning.

**Code Example:**
```solidity
function updateAll(uint[] memory ids, uint value) public {
    for (uint i = 0; i < ids.length; i++) {
        items[ids[i]].value = value;
    }
}

```
**Expected AI Output:**

Looping over an array is fine, but gas cost scales linearly with size.

No bounds check — ensure ids.length is reasonable.

Consider using unchecked {} for the increment if overflow isn't possible.

Could batch updates off-chain and call fewer on-chain transactions.

Suggestion: Cache ids.length in a local variable.


## What I Learnt

Chain of Thought helps AI simulate real reasoning. its great for teaching, debugging and threat modeling.

It produces more accurate answers in complex logic scenarios.

Applying CoT with Solidity makes LLMs feel more like mentors or security partners.


## Tools Used
OpenAI and Claude

VS Code with WSL

Remix IDE for testing logic


[Repo](github.com/sortlight/ai-prompt-learning)

## Coming Next: Day 4 — Persona Prompting for Security & Productivity
Next I’ll explore how to create custom AI personas (e.g., “DeFi risk analyst,” “Web3 project manager,” or “Christian coder coach”) that reflect my workflow and value as a person. 


Stay blessed!
SortSec
