# 🧙‍♂️ Day 2 – Role-Based Prompting

## 🧠 What I Learned
Today I learned how to use **role-based prompting** to shape the voice, style, and depth of AI responses. This technique allows me to assign a "persona" to the AI so that it responds more appropriately for specialized tasks.

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
