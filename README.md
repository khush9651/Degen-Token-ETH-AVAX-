# Degen Token (ERC-20): Unlocking the Future of Gaming

The Degen Token Project is a Solidity-based smart contract that implements an ERC20 token named "Degen" with the symbol "DGN". It includes functionalities for minting 
new tokens, burning existing tokens, managing ownership, and facilitating token transfers according to the ERC20 standard. Additionally, it supports pausing and unpausing 
of contract operations for enhanced security.

## Description
The Degen Token Project is designed to provide a robust and flexible ERC20 token contract with added features for minting and burning tokens, pausing contract 
operations, and managing ownership. The contract allows the owner to mint new tokens, burn tokens from any account, and redeem tokens with additional custom logic. 
It is built using OpenZeppelin's library for secure and efficient smart contract development. The project aims to be a comprehensive solution for any application 
requiring a custom ERC20 token with advanced management capabilities.

## Getting Started

### Installing
To get started with the Mint Token Project, follow these steps:

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/Degen-Token-Project.git
    cd Degen-Token-Project
    ```

2. Install the required dependencies:
    ```bash
    npm install
    ```

### Executing Program
To run this program, you can use Remix, an online Solidity IDE. Follow these steps:

1. Go to the Remix website at [Remix Ethereum](https://remix.ethereum.org/).

2. Create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a `.sol` extension (e.g., `DegenToken.sol`). Copy and paste the
   following code into the file:

    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;

    import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
    import "@openzeppelin/contracts/security/Pausable.sol";
    import "@openzeppelin/contracts/access/Ownable.sol";

    contract DegenToken is ERC20, Pausable, Ownable {
        event TokensRedeemed(address indexed user, uint256 amount, string note);

        constructor() ERC20("Degen", "DGN") Ownable(msg.sender) {
            _mint(msg.sender, 1000000 * 10 ** decimals());
        }

        function mint(address to, uint256 amount) external onlyOwner whenNotPaused {
            _mint(to, amount);
        }

        function redeem(uint256 amount, string calldata note) external whenNotPaused {
            require(balanceOf(msg.sender) >= amount, "Insufficient balance to redeem");
            _burn(msg.sender, amount);
            emit TokensRedeemed(msg.sender, amount, note);
            // Implement additional redemption logic here, e.g., rewarding in-game items
        }

        function burn(uint256 amount) external whenNotPaused {
            _burn(msg.sender, amount);
        }

        function pause() external onlyOwner {
            _pause();
        }

        function unpause() external onlyOwner {
            _unpause();
        }
    }
    ```

4. Compile the code:
    - Click on the "Solidity Compiler" tab in the left-hand sidebar.
    - Make sure the "Compiler" option is set to "0.8.0" (or another compatible version).
    - Click on the "Compile DegenToken.sol" button.

5. Deploy the contract:
    - Click on the "Deploy & Run Transactions" tab in the left-hand sidebar.
    - Select the "DegenToken" contract from the dropdown menu.
    - Click on the "Deploy" button.

6. Interact with the deployed contract:
    - Click on the "DegenToken" contract in the left-hand sidebar.
    - You can now call functions such as `mint`, `burn`, and `redeem` by providing the required inputs and clicking on the appropriate buttons.

    For example, to mint tokens:
    - Select the `mint` function.
    - Provide the recipient address and amount.
    - Click on the "transact" button.

    To redeem tokens:
    - Select the `redeem` function.
    - Provide the amount and a note.
    - Click on the "transact" button.

    To burn tokens:
    - Select the `burn` function.
    - Provide the amount.
    - Click on the "transact" button.


## Help
For common problems or issues, consider the following:

- Ensure you have the correct version of Node.js and npm installed.
- Check if your local blockchain instance (e.g., Hardhat Network) is running.
- Verify that your wallet address has sufficient ETH for transaction fees.

If the program contains helper info, you can run the following command:
```bash
npx hardhat help
```
# LICENSE
This project is licensed under the MIT License - see the LICENSE.md file for details
