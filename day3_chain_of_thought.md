#  Day 3: Chain-of-Thought (CoT) Prompting Step by Step Reasoning

Today’s focus was **Chain of Thought prompting** which guides the AI to reason step by step instead of jumping to conclusions. This is super helpful when analyzing smart contract logic, debugging and explaining attacker flow.

---

##  Prompt 1: Solidity Debugging — CoT Style

**Prompt:**  
You are a Solidity tutor. I will paste a function, and I want you to walk through the logic line by line. If there are issues, explain how they could cause errors or vulnerabilities. Think step-by-step and reason like you're explaining to a junior dev.

Expected AI Output:

✅ Check: Buyer must send at least 1 ETH.

🧮 Divides ETH sent by tokenPrice to calculate how many tokens to give.

⚠️ If tokenPrice == 0, this causes a division by zero error.

❗ No check if contract has enough tokens to sell.

🔥 Could fail if owner is a contract that rejects Ether.

✅ Improvement: Add check for contract token balance before updating balances.

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



