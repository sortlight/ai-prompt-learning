# Day 6: Style Transfer & Code Documentation: Make AI Speak Your Language

Today's focus: **Style Transfer + AI-assisted Documentation**

Style transfer lets me guide the AI to write in **specific tones**, voices or formats. Especially from technical docs to Twitter threads, from friendly tutors to streetwise devs.

Documentation prompting helps the AI **auto-write explanations** for functions, smart contracts or full projects in a tone that fits the context: academic, chill, startup-friendly or even spiritually infused.

---

##  Prompt 1: Explain Code Like a startup Engineer

**Prompt:**  
You are a Web3 engineer writing public documentation for a DeFi protocol. I’ll paste a Solidity function. Kindly explain it clearly, in plain English with some dev humor.

**Code Example:**
```solidity

function stake(uint _amount) public {
    require(balanceOf[msg.sender] >= _amount, "Not enough tokens");
    staked[msg.sender] += _amount;
    balanceOf[msg.sender] -= _amount;
}

```
**Expected AI Output:**



    > This function lets users lock up tokens for staking. First, we check that the user has enough tokens. Then we increase their staked balance and subtract the same amount from their wallet.
    > TL;DR: No stake, no gain. Bring your own balance.


## Prompt 2: Style Transfer: Speak Like Me

**Prompt:**
You’re a cool Nigerian tech bro who blends Web3, faith, and purpose. Explain the code in a laid-back tone, with spiritual depth but no cringe. I’ll paste Solidity — you explain what it does and why it matters to someone building kingdom tech.

**Code Example:**
```solidity
    > function mint(address to, uint256 amount) public onlyOwner {
    totalSupply += amount;
    balanceOf[to] += amount;
    }
```

**Expected AI Output:**

    > So boom — this function lets the contract owner mint new tokens. We’re increasing the total supply and crediting someone’s wallet. Simple.
    > Spiritually? Think of it like divine provision — when the Source decides it’s time to expand capacity. But with great power comes supply cap

## Prompt 3: Auto-Generate Function Comments
Prompt:
I’ll paste a Solidity smart contract. Generate clean, professional inline comments above each function and logic block — suitable for open source projects.

**Code Example:**
```solidity
    > contract Vault {
    mapping(address => uint) public deposits;

    function deposit() public payable {
        deposits[msg.sender] += msg.value;
    }

    function withdraw(uint amount) public {
        require(deposits[msg.sender] >= amount, "Insufficient balance");
        deposits[msg.sender] -= amount;
        payable(msg.sender).transfer(amount);
    }
}

```
**Expected AI Output:**
```solidity
      > // Stores the ETH deposits of each user
mapping(address => uint) public deposits;

// Allows users to deposit ETH into the vault
function deposit() public payable {
    deposits[msg.sender] += msg.value;
}

// Allows users to withdraw their ETH if they have enough balance
function withdraw(uint amount) public {
    require(deposits[msg.sender] >= amount, "Insufficient balance");
    deposits[msg.sender] -= amount;
    payable(msg.sender).transfer(amount);
}

```

What I Learnt
1. Prompting the AI with a tone and purpose gives humanized content

2. AI can auto-generate code docs, but I control the voice

3. Whether it’s a LinkedIn post, a README, or a code comment, style matters

4. I can make my documentation brand-aligned, faithful or fun

**Tools Used**

ChatGPT (GPT-4)

Solidity + Remix

My personal voice & coding style

 **Repo link **
 
[Ai prompt learning](github.com/sortlight/ai-prompt-learning)

# Up Next: Day 7 — Multi-Shot Prompting + Prompt Memory
Next I’ll dive into how to feed multiple examples into the prompt (multi-shot) and simulate “memory” for larger tasks or contextual understanding.

Let’s build smarter flows


