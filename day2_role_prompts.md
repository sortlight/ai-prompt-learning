#  Day 2 – Role-Based Prompting

## What I Learned
Today I learned how to use **role-based prompting** to shape the style and depth of AI responses. This technique allows me to assign a "persona" to the AI so that it responds more appropriately for specialized tasks.

By saying things like "Act as a UX designer" or "Act as a software engineer", the output becomes far more focused, accurate, and natural.

---

## 🔧 Prompt 1 – Developer Role

**Prompt:**  
Act as a senior smart contract auditor. I’ll paste a Solidity function, and I want you to identify potential bugs and security issues.

**Code Example:**  
```solidity
function withdraw(uint amount) public {
    require(msg.sender == owner);
    if (amount <= address(this).balance) {
        payable(msg.sender).transfer(amount);
    }
}


## 3. Paste into ChatGPT (or your AI agent)

It will return something like:

>  **Security Risks Identified:**
> 1. **Reentrancy Vulnerability**: `msg.sender.call{value: amount}("")` sends funds **before** updating the balance.
> 2. **Missing Checks-Effects-Interactions Pattern**.
> 3. **No Events Emitted** after withdrawal.

##  Optional: Use a safer version for comparison




```solidity
function withdraw(uint amount) public {
    require(balances[msg.sender] >= amount);
    balances[msg.sender] -= amount;
    (bool success, ) = msg.sender.call{value: amount}("");
    require(success);
}

