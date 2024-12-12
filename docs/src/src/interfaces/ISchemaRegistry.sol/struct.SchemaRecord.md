# SchemaRecord
[Git Source](https://github.com/RafaDSan/trustful-zuzalu-contracts/blob/8145173dbd34bc00952ca1adb04b16dbe11ff624/src/interfaces/ISchemaRegistry.sol)

A struct representing a record for a submitted schema.


```solidity
struct SchemaRecord {
    bytes32 uid;
    IResolver resolver;
    bool revocable;
    string schema;
}
```

