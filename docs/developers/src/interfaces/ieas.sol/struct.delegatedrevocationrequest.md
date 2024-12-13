# DelegatedRevocationRequest
[Git Source](https://github.com/RafaDSan/trustful-zuzalu-contracts/blob/8145173dbd34bc00952ca1adb04b16dbe11ff624/src/interfaces/IEAS.sol)

A struct representing the arguments of the full delegated revocation request.


```solidity
struct DelegatedRevocationRequest {
    bytes32 schema;
    RevocationRequestData data;
    Signature signature;
    address revoker;
    uint64 deadline;
}
```

