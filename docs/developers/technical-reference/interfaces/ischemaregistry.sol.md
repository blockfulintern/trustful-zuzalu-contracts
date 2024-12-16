# ISchemaRegistry.sol

[Git Source](https://github.com/RafaDSan/trustful-zuzalu-contracts/blob/8145173dbd34bc00952ca1adb04b16dbe11ff624/src/interfaces/ISchemaRegistry.sol)

**Inherits:** [ISemver](../../../../src/interfaces/ISemver.sol/interface.ISemver.md)

The interface of global attestation schemas for the Ethereum Attestation Service protocol.

## Functions

### register

Submits and reserves a new schema

```solidity
function register(string calldata schema, IResolver resolver, bool revocable) external returns (bytes32);
```

**Parameters**

| Name        | Type        | Description                                       |
| ----------- | ----------- | ------------------------------------------------- |
| `schema`    | `string`    | The schema data schema.                           |
| `resolver`  | `IResolver` | An optional schema resolver.                      |
| `revocable` | `bool`      | Whether the schema allows revocations explicitly. |

**Returns**

| Name     | Type      | Description                |
| -------- | --------- | -------------------------- |
| `<none>` | `bytes32` | The UID of the new schema. |

### getSchema

Returns an existing schema by UID

```solidity
function getSchema(bytes32 uid) external view returns (SchemaRecord memory);
```

**Parameters**

| Name  | Type      | Description                        |
| ----- | --------- | ---------------------------------- |
| `uid` | `bytes32` | The UID of the schema to retrieve. |

**Returns**

| Name     | Type           | Description              |
| -------- | -------------- | ------------------------ |
| `<none>` | `SchemaRecord` | The schema data members. |

## Events

### Registered

Emitted when a new schema has been registered

```solidity
event Registered(bytes32 indexed uid, address indexed registerer, SchemaRecord schema);
```

**Parameters**

| Name         | Type           | Description                                             |
| ------------ | -------------- | ------------------------------------------------------- |
| `uid`        | `bytes32`      | The schema UID.                                         |
| `registerer` | `address`      | The address of the account used to register the schema. |
| `schema`     | `SchemaRecord` | The schema data.                                        |
