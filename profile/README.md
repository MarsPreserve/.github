# Welcome to Mars Preserve Research Foundation 🍊

Welcome to The Mars Preserve Research Foundation. Our mission is to manage, build, create, and serve a meaningful purpose by delivering digital products, assets, and NFTs. This project (currently in BETA) focuses on developing AutoGrowBoxes for growing food and other desired herbs. However, space and a structured organization are required before the minting process can be initiated.

We are building on the Polygon network. If the need arises to switch blockchains, we will reissue the minting process and remove our listings from the current service network.

These new Digital Assets and NFTs will allow you to stay updated on the project's progress. I plan to work on this project independently, raising capital and minting new assets under my own brand and organization. This approach will provide legitimacy and a strong foundation for the project.

Why use the Polygon network? Because their platform makes it easy to mint tokens on a blockchain with lower gas fees, which is essential for cost efficiency.

This project requires time, effort, and patience. For me, it’s about learning from my mistakes and growing through the process. I believe I am on the right path. As the project progresses and the foundation is established, I aim to create a platform where people can share, collaborate, and develop their own projects in alignment with our brand: The Mars Preserve Research Foundation.

If you have any questions, comments, or suggestions, or if you’re interested in this project or my profile, I’d be happy to discuss these topics further.

I hope this resonates with you and inspires your own ideas about the vision I have for The Mars Preserve Research Foundation and the AutoGrowBoxes project.

Thank you, and let me know your thoughts!

# Mars Preserve Research ( Smart Contract source code )

```

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
import "@openzeppelin/contracts/security/Pausable.sol";
import "@openzeppelin/contracts/access/AccessControl.sol";

contract AdvancedMintableToken is ERC20, ERC20Burnable, Pausable, AccessControl {
    bytes32 public constant MINTER_ROLE = keccak256("MINTER_ROLE");
    uint256 public immutable cap;

    event Mint(address indexed to, uint256 amount);
    event Paused(address account);
    event Unpaused(address account);

    constructor(
        string memory name,
        string memory symbol,
        uint256 _cap,
        address admin
    ) ERC20(name, symbol) {
        require(_cap > 0, "Cap must be greater than zero");
        cap = _cap;

        _grantRole(DEFAULT_ADMIN_ROLE, admin);
        _grantRole(MINTER_ROLE, admin);
    }

    function mint(address to, uint256 amount) public onlyRole(MINTER_ROLE) whenNotPaused {
        require(totalSupply() + amount <= cap, "Cap exceeded");
        _mint(to, amount);
        emit Mint(to, amount);
    }

    function pause() public onlyRole(DEFAULT_ADMIN_ROLE) {
        _pause();
        emit Paused(msg.sender);
    }

    function unpause() public onlyRole(DEFAULT_ADMIN_ROLE) {
        _unpause();
        emit Unpaused(msg.sender);
    }

    // Override _beforeTokenTransfer to respect pause state
    function _beforeTokenTransfer(address from, address to, uint256 amount)
        internal
        override
        whenNotPaused
    {
        super._beforeTokenTransfer(from, to, amount);
    }
}




```

# 🌌 Mars Preserve Research Foundation Token (MPRFT) Digital Asset Holdings

## Overview

The **Mars Preserve Research Foundation Token (MPRFT)** is a blockchain-based initiative and project seeking to focus on funding and supporting efforts to preserve and explore Mars. 
This token is designed to incentivize contributions to Mars-related projects and create a decentralized ecosystem for collaboration funding the Mars Preserve Research Foundation.

## Features

- **Decentralized Governance**: Token holders can vote on Mars-related projects and initiatives.
- **Smart Contracts**: Built on **Ethereum** using **Solidity** for secure and transparent transactions.
- **Sustainability**: A portion of every transaction is allocated to Mars preservation and exploration funds.

## Tokenomics

- **Token Name**: Mars Preserve Research Foundation Token (unit allocation creation)
- **Symbol**: MPT
- **Total Supply**: 1,000,000,000 MPRFT requested allocation of units

- **Distribution**: Available when project is initialized
  
  - 25% for public sale blockchain public network utility 
  - 25% for private sale peer 2 peer
  - 25% for RND (R N D)
  - 25% for Taxes
    
### Project Details

The Mars Preserve Research Foundation Token (MPRFT) project is dedicated to supporting Mars exploration and preservation efforts through blockchain technology. Key details include:

- **Mission**: To create a decentralized ecosystem that funds Mars-related research and initiatives.

- **Technology**: Built on the **Ethereum** blockchain using **Solidity** for smart contracts.
- **Focus Areas**:
  - Funding Mars preservation projects.
  - Supporting research for sustainable Mars exploration.
  - Building a community of contributors and enthusiasts.

# Understanding Polygon Network, Layer 2, and Gas Fees

## What is the Polygon Network? 
## Building on Polygon Network

The **Polygon Network** (formerly known as Matic Network) is a Layer 2 scaling solution for Ethereum. It is designed to improve the scalability, speed, and cost-efficiency of blockchain transactions while maintaining compatibility with the Ethereum ecosystem.

### Key Features of Polygon:
1. **Scalability**:
   - Polygon enables faster and cheaper transactions by processing them off the Ethereum mainnet and then settling them back on Ethereum.
   
2. **Interoperability**:
   - Polygon supports interoperability between Ethereum and other blockchains, allowing seamless communication and asset transfers.

3. **Security**:
   - Polygon uses Ethereum's robust security model while providing its own additional security layers.

4. **Developer-Friendly**:
   - Polygon offers tools and frameworks for developers to build decentralized applications (DApps) with ease.

---

## What is Layer 2?

**Layer 2** refers to a secondary framework or protocol built on top of an existing blockchain (Layer 1, such as Ethereum). The purpose of Layer 2 solutions is to address the scalability and performance limitations of the base blockchain.

### Benefits of Layer 2:
1. **Reduced Congestion**:
   - By processing transactions off-chain, Layer 2 reduces the load on the main blockchain, preventing network congestion.

2. **Lower Gas Fees**:
   - Transactions on Layer 2 are significantly cheaper compared to Layer 1, making it more accessible for users.

3. **Faster Transactions**:
   - Layer 2 solutions process transactions much faster, enabling real-time interactions for DApps and users.

4. **Enhanced User Experience**:
   - With lower costs and faster speeds, Layer 2 improves the overall user experience for blockchain applications.

---

## What are Gas Fees?

**Gas fees** are the transaction fees paid to miners or validators for processing and validating transactions on a blockchain. These fees are essential for maintaining the network's security and incentivizing participants.

### How Gas Fees Work:
1. **Gas Units**:
   - Each operation on the blockchain (e.g., transferring tokens, executing smart contracts) requires a certain amount of computational effort, measured in gas units.

2. **Gas Price**:
   - The gas price is the amount users are willing to pay per gas unit, typically measured in Gwei (a fraction of Ethereum).

3. **Total Gas Fee**:
   - The total gas fee is calculated as:
     ```
     Gas Fee = Gas Units × Gas Price
     ```

### Why Gas Fees Matter:
1. **Network Security**:
   - Gas fees incentivize miners or validators to process transactions and secure the network.

2. **Transaction Prioritization**:
   - Users can set higher gas prices to prioritize their transactions during times of network congestion.

3. **Cost Barrier**:
   - High gas fees on Layer 1 (Ethereum) can make blockchain usage expensive, especially for smaller transactions.

---

## How Polygon Reduces Gas Fees

The Polygon Network significantly reduces gas fees by processing transactions on its Layer 2 infrastructure instead of the Ethereum mainnet. Here’s how it works:

1. **Batch Processing**:
   - Polygon batches multiple transactions together and submits them to Ethereum as a single transaction, reducing the overall cost.

2. **Off-Chain Execution**:
   - Most of the computational work is done off-chain, where gas fees are much lower.

3. **Optimized Architecture**:
   - Polygon’s architecture is designed to minimize resource usage, further reducing transaction costs.

---

## Why Use Polygon and Layer 2?

1. **Cost Efficiency**:
   - Polygon drastically lowers gas fees, making it ideal for microtransactions, gaming, and DeFi applications.

2. **Scalability**:
   - With faster transaction speeds, Polygon supports high-throughput applications without compromising performance.

3. **Ethereum Compatibility**:
   - Polygon is fully compatible with Ethereum, allowing developers to migrate their DApps seamlessly.

4. **Sustainability**:
   - By reducing the computational load on Ethereum, Polygon contributes to a more sustainable blockchain ecosystem.

---

## Conclusion

The **Polygon Network** and other **Layer 2 solutions** are revolutionizing the blockchain space by addressing the scalability and cost challenges of Layer 1 blockchains like Ethereum. By significantly reducing **gas fees** and improving transaction speeds, Polygon is paving the way for mass adoption of blockchain technology.

## Why it matters

If you're building or using blockchain applications, exploring Layer 2 solutions like Polygon can provide a more efficient and cost-effective experience.

---

## Roadmap

1. **Phase 1**: Token Development

   - Smart contract creation and deployment.
   - Initial token distribution.
   - allocation of new express business brands.

2. **Phase 2**: Project Building

   - Buy connex shipping HC containers.
   - Build partnerships with Mars-focused organizations.
   - create new sponsorship stickers. (NFT printables)

3. **Phase 3**: DIY and Expansion of Project
    - Build AutoGrowBox After Foundation is built.
    - Sell AutoGrowBox Brand Under Mars Preserve Research Foundation.

## FAQ

### What are digital assets?

Digital assets are electronic files or tokens that hold value and can be owned or transferred digitally. 

Examples include:

- Bitcoin Without the crazy mathematics. Purpose Built. Research Development.
- Non-Fungible Tokens (NFTs) representing unique digital items. See Ref AutoGrowBoxes
- Digital representations of real-world assets, such as tokenized real estate or art. Digital Assets Holdings.

### What is a blockchain network?

A blockchain network is a decentralized, distributed ledger technology that records transactions across multiple computers. 

Key features include:

- **Transparency**: All transactions are visible to participants in the network.

- **Security**: Data is secured using cryptographic algorithms.

- **Immutability**: Once recorded, transactions cannot be altered or deleted.

- **Decentralization**: No single entity controls the network, ensuring trust and resilience.



### What is a Software Insurance Policy?

A software insurance policy is a form of protection that ensures compensation or support in case of software-related issues, such as:

- **Data Loss**: Coverage for accidental loss of critical data.

- **Cybersecurity Breaches**: Protection against hacking or unauthorized access.

- **Service Downtime**: Compensation for losses due to software outages or failures.

- **Liability Coverage**: Protection against claims arising from software defects or misuse.


# 🌱 AutoGrowBox

The **AutoGrowBox** is an innovative, small, efficient, and accessible automation grow box designed to revolutionize farming and gardening. It provides a controlled environment for plants to thrive, making it easier for farmers, gardeners, and enthusiasts to grow crops efficiently, to be sustainable and automate the grow process leaving the farmer time to plant more crops.Automation Grow Boxes for Mars Preserve Research Foundation ( Creative Commons Share Alike Attribute too ) NOT MIT.

---

## 🚀 Features

### Efficient Design

- Compact and space-saving design suitable for small spaces.
- Energy-efficient components to reduce power consumption.
- Modular structure for easy assembly and maintenance.

### Accessible Features

- User-friendly interface for monitoring and controlling the grow box.
- Affordable materials to ensure accessibility for all users.
- Designed to be lightweight and portable.

### Automate Growth

- Automated watering, lighting, and nutrient delivery systems.
- Sensors to monitor temperature, humidity, and soil moisture levels.
- AI-driven algorithms to optimize plant growth cycles.

### Controlled Environment

- Fully enclosed system to protect plants from pests and external factors.
- Adjustable climate controls for temperature, humidity, and light intensity.
- Real-time monitoring and alerts for environmental changes.

---

## Contact

For more information, about the project and research foundation I am starting, visit [GitHub.com/MarsPreserve](https://github.com/marspreserve) or reach out to Cody Bunnell at @Coderad32 via Github.com

**Made with ❤️ by [Coderad32](https://github.com/Coderad32)** Founder of Mars Preserve Research Foundation all rights reserved 2025-BeyondTheViewport Creative Commons Share Alike Attribute Too.
