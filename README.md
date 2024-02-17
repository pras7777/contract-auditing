# contract-auditing

#### Summary:
The contract `StorageVictim` has been audited to assess its security and efficiency. The audit aimed to identify vulnerabilities, areas of improvement, and potential risks associated with the contract.

#### Findings:

1. Uninitialized Storage Pointer:
   - In the original contract, the `store` function uses an uninitialized storage pointer, which could lead to unexpected behavior.
   - The pointer `str` is not initialized before use, causing it to point to the storage address 0 by default, which is the `owner` variable.
   - This could potentially overwrite the `owner` address when the `store` function is called.

#### Recommendations:

1. Initialize Storage Pointer:
   - Initialize the `str` storage pointer directly from the `storages` mapping to avoid unintended behavior.
   - By directly assigning `storages[msg.sender]` to `str`, the pointer will correctly point to the storage location associated with the caller's address.

### Fixes:

1. Initialize Storage Pointer:
   - Update the `store` function to directly initialize the `str` storage pointer from the `storages` mapping.

```solidity
function store(uint256 _amount) public {
    Storage storage str = storages[msg.sender];
    str.user = msg.sender;
    str.amount = _amount;
}
```

### Conclusion:
The contract `StorageVictim` has been assessed for security vulnerabilities and provided with recommendations for improvement. By implementing the suggested fixes, the contract's reliability and security can be enhanced. Testing on a testnet environment is recommended to ensure the correctness and functionality of the updated contract.

#### Contract Description:
The `StorageVictim` contract stores user addresses and corresponding amounts in a mapping. It also allows users to retrieve their stored address and amount, along with providing the contract owner's address.

#### Installation Instructions:
1. Deploy the `StorageVictim` contract on a testnet environment using a compatible Ethereum development tool like Remix or Truffle.
2. Interact with the deployed contract using a compatible Ethereum wallet or through a decentralized application (DApp) interface.

#### Usage:
- Call the `store` function to store an amount associated with the caller's address.
- Call the `getStore` function to retrieve the caller's stored address and amount.
- Call the `getOwner` function to retrieve the contract owner's address.

#### Audit Report:
- Review the provided audit report for security vulnerabilities and recommended fixes.
- Implement the suggested fixes to enhance the contract's security and reliability.

#### Testnet Deployment:
- Deploy the `StorageVictim` contract on a testnet environment for testing and validation purposes.
- Ensure that the contract functions as expected and addresses any identified issues before deploying to the mainnet.
