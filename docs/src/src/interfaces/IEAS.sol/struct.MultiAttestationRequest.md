# MultiAttestationRequest
[Git Source](https://github.com/RafaDSan/trustful-zuzalu-contracts/blob/8145173dbd34bc00952ca1adb04b16dbe11ff624/src/interfaces/IEAS.sol)

A struct representing the full arguments of the multi attestation request.


```solidity
struct MultiAttestationRequest {
    bytes32 schema;
    AttestationRequestData[] data;
}
```
