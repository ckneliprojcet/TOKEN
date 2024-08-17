# MyToken Smart Contract

The `MyToken` smart contract is an ERC-20 token with added functionality for burning, pausing, and ownership control. It uses OpenZeppelin's secure and battle-tested libraries to provide standard token operations, along with some extended features.

## Features

- **ERC-20 Standard:** Implements the basic ERC-20 token standard.
- **Burnable:** Allows the owner to burn tokens, reducing the total supply.
- **Pausable:** The owner can pause all token transfers, useful in emergency situations.
- **Ownership Management:** The contract owner has special permissions and can transfer ownership to another address.

## Token Details

- **Token Name:** yinkadesmond
- **Token Symbol:** YNKDSMD
- **Decimals:** 18 (standard for ERC-20 tokens)

## Contract Functions

### `constructor(address initialOwner)`

Initializes the token with the specified owner and sets the token's name and symbol.

- `initialOwner`: The address that will be the initial owner of the contract.

### `pause() public onlyOwner`

Pauses all token transfers. This function can only be called by the owner.

### `unpause() public onlyOwner`

Resumes all token transfers. This function can only be called by the owner.

### `mint(address to, uint256 amount) public onlyOwner`

Mints new tokens and assigns them to the specified address.

- `to`: The address that will receive the minted tokens.
- `amount`: The number of tokens to mint.

### `burn(address account, uint256 amount) public onlyOwner`

Burns a specified number of tokens from the specified address, reducing the total supply.

- `account`: The address from which tokens will be burned.
- `amount`: The number of tokens to burn.

### `transfer(address recipient, uint256 amount) public override returns (bool)`

Transfers tokens from the caller's address to the specified recipient.

- `recipient`: The address that will receive the tokens.
- `amount`: The number of tokens to transfer.

### `approve(address spender, uint256 amount) public override returns (bool)`

Approves the specified spender to spend a specified number of tokens on behalf of the caller.

- `spender`: The address that will be allowed to spend tokens.
- `amount`: The maximum number of tokens that can be spent.

### `transferFrom(address sender, address recipient, uint256 amount) public override returns (bool)`

Transfers tokens from one address to another, using the allowance mechanism.

- `sender`: The address to transfer tokens from.
- `recipient`: The address to transfer tokens to.
- `amount`: The number of tokens to transfer.

### `allowance(address owner, address spender) public view override returns (uint256)`

Returns the remaining number of tokens that the spender is allowed to spend on behalf of the owner.

- `owner`: The address that owns the tokens.
- `spender`: The address that can spend the tokens.

### `changeOwner(address newOwner) public onlyOwner`

Transfers ownership of the contract to a new address.

- `newOwner`: The address that will become the new owner of the contract.

## Events

- **`Transfer(address indexed from, address indexed to, uint256 value)`**: Emitted when tokens are transferred, including zero-value transfers.
- **`Approval(address indexed owner, address indexed spender, uint256 value)`**: Emitted when the allowance of a spender for an owner is set by a call to `approve`.
- **`OwnershipTransferred(address indexed previousOwner, address indexed newOwner)`**: Emitted when the contract ownership is transferred to a new owner.
- **`Paused(address account)`**: Emitted when the contract is paused.
- **`Unpaused(address account)`**: Emitted when the contract is unpaused.

## Security Considerations

- **Ownership Control:** Only the owner can mint, burn, pause, or unpause the token, providing centralized control over these sensitive operations.
- **Pausable:** The pause functionality can be used to halt all token transfers in the event of an emergency.

## License

This project is licensed under the MIT License.



## Getting Started
- npm start

### Prerequisites

- Solidity compiler version ^0.8.19
- Node.js and npm (for deploying via scripts)
- Truffle or Hardhat (for testing and deployment)
- MetaMask or any other Ethereum-compatible wallet

### Installing

1. Clone the repository:

   ```bash
   git clone https://github.com/your-repo/mytoken.git
   cd mytoken

 ## Contract Code

 ### Executing program

```javascript
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Pausable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyToken is ERC20, ERC20Burnable, ERC20Pausable, Ownable {
    constructor(address initialOwner)
        ERC20("yinkadesmond", "YNKDSMD")
        Ownable(initialOwner)
    {}

    function pause() public onlyOwner {
        _pause();
    }

    function unpause() public onlyOwner {
        _unpause();
    }

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }

    function burn(address account, uint256 amount) public onlyOwner {
        _burn(account, amount);
    }

    function transfer(address recipient, uint256 amount) public override returns (bool) {
        _transfer(_msgSender(), recipient, amount);
        return true;
    }

    function approve(address spender, uint256 amount) public override returns (bool) {
        _approve(_msgSender(), spender, amount);
        return true;
    }

    function transferFrom(
        address sender,
        address recipient,
        uint256 amount
    ) public override returns (bool) {
        _transfer(sender, recipient, amount);
        _approve(
            sender,
            _msgSender(),
            allowance(sender, _msgSender()) - amount
        );
        return true;
    }

    function allowance(address owner, address spender) public view override returns (uint256) {
        return super.allowance(owner, spender);
    }

    function changeOwner(address newOwner) public onlyOwner {
        require(newOwner != address(0), "New owner is the zero address");
        transferOwnership(newOwner);
    }

    function _update(address from, address to, uint256 value)
        internal
        override(ERC20, ERC20Pausable)
    {
        super._update(from, to, value);
    }
}


```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.19" (or another compatible version), and then click on the "Compile HelloWorld.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "HelloWorld" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by calling the sayHello function. Click on the "HelloWorld" contract in the left-hand sidebar, and then click on the "sayHello" function. Finally, click on the "transact" button to execute the function and retrieve the "Hello World!" message.


This file provides a comprehensive overview of your smart contract, including the code, usage instructions, and additional details.
