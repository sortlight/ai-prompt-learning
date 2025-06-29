#  Day 2: Role-Based Prompt Engineering — Smart Contract Security

In this challenge, I explored **role-based prompting** assigning expert identities to the AI to guide its response style and technical depth. This technique helps unlock more relevant, focused outputs from language models especially useful in complex fields like Web3 security.

For Day 2, I crafted 3 role-specific prompts using Solidity smart contract examples.

---

## Prompt 1:  Smart Contract Auditor

**Prompt:**  
Act as a senior smart contract auditor. I’ll paste a Solidity function, and I want you to identify potential bugs and security issues.

Expected AI Output:

⚠️ Reentrancy vulnerability: Funds are sent before updating the balance.

🧱 Breaks the Checks-Effects-Interactions pattern.

✅ Fix: Update the balance before sending the Ether.

📉 No event emission for withdraw.



#  Prompt 2:  Bug Bounty Hunter
Prompt:
Act as an experienced bug bounty hunter analyzing Solidity smart contracts on live DeFi platforms. I’ll paste a function — your task is to identify any vulnerability, suggest a real-world exploit scenario, and recommend a patch or refactor.

Expected AI Output:

Vulnerable to reentrancy: User’s balance is updated after the external call.

Exploit scenario: Malicious contract reenters claim() via fallback before balance reset.

Patch: Apply Checks-Effects-Interactions. Move balances[msg.sender] = 0 before sending Ether.

Also consider using transfer() or send() for better gas-limited protection.


 #  Prompt 3: Gas Optimization Expert
Prompt:
Act as a Solidity gas optimization expert. I’ll paste a smart contract function — your task is to suggest gas-saving improvements without compromising functionality.


Expected AI Output:

🔁 Cache values.length outside the loop to save gas.

💾 Consider maintaining a running total variable to avoid recalculating sums.

❗ Use custom errors instead of require() strings to save gas.

📉 Use unchecked {} for the loop increment if overflow isn’t possible.

✅ Key Takeaways
🧠 Giving the AI a specific expert identity changes its behavior dramatically.

🔍 Role-based prompting is useful for security audits, exploit simulation, and gas optimization.

🚀 These techniques can enhance smart contract reviews, training, and automated static analysis using LLMs.



# ** Stack Used:**

GPT-4

Markdown + Git

WSL (Ubuntu) + VS Code

⚙GitHub

Solidity (tested via Remix IDE)

GitHub Repo




# **Up Next:** Day 3. Chain-of-Thought Prompting
Next I’ll explore how to make the AI reason step-by-step using Chain-of-Thought prompting. Very Useful for logic-heavy tasks, debugging and structured problem-solving.

Stay blessed!
SortSec

Code Example:
```solidity
function withdraw(uint amount) public {
    require(balances[msg.sender] >= amount);
    (bool success, ) = msg.sender.call{value: amount}("");
    require(success);
    balances[msg.sender] -= amount;
}


#  Prompt 2: 👾 Bug Bounty Hunter
Prompt:
Act as an experienced bug bounty hunter analyzing Solidity smart contracts on live DeFi platforms. I’ll paste a function — your task is to identify any vulnerability, suggest a real-world exploit scenario, and recommend a patch or refactor.

Code Example:

solidity
Copy
Edit
mapping(address => uint256) public balances;

function deposit() public payable {
    balances[msg.sender] += msg.value;
}

function claim() public {
    uint256 amount = balances[msg.sender];
    require(amount > 0, "No funds to claim");

    (bool sent, ) = msg.sender.call{value: amount}("");
    require(sent, "Failed to send Ether");

    balances[msg.sender] = 0;
}


🎯 Prompt 3: ⛽ Gas Optimization Expert
Prompt:
Act as a Solidity gas optimization expert. I’ll paste a smart contract function — your task is to suggest gas-saving improvements without compromising functionality.

Code Example:

solidity
Copy
Edit
uint[] public values;

function addValue(uint value) public {
    require(value > 0);
    values.push(value);
}

function sumValues() public view returns (uint) {
    uint sum = 0;
    for (uint i = 0; i < values.length; i++) {
        sum += values[i];
    }
    return sum;
}


