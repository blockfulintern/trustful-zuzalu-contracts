# Common.sol

### Signature Struct

A struct representing ECDSA signature data.

```solidity
struct Signature {
    uint8 v;
    bytes32 r;
    bytes32 s;
}
```

### Attestation Struct

A struct representing a single attestation.

```solidity
struct Attestation {
    bytes32 uid;
    bytes32 schema;
    uint64 time;
    uint64 expirationTime;
    uint64 revocationTime;
    bytes32 refUID;
    address recipient;
    address attester;
    bool revocable;
    bytes data;
}
```

### uncheckedInc function

A helper function to work with unchecked iterators in loops.

```solidity
function uncheckedInc(uint256 i) pure returns (uint256 j);
```
