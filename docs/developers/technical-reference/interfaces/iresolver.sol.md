# IResolver.sol

[Git Source](https://github.com/RafaDSan/trustful-zuzalu-contracts/blob/8145173dbd34bc00952ca1adb04b16dbe11ff624/src/interfaces/IResolver.sol)

The interface of the {Resolver} contract.

## Functions

### isPayable

Checks if the resolver can be sent ETH.

```solidity
function isPayable() external pure returns (bool);
```

**Returns**

| Name     | Type   | Description                                  |
| -------- | ------ | -------------------------------------------- |
| `<none>` | `bool` | Whether the resolver supports ETH transfers. |

### allowedAttestationTitles

_Checks if a title is allowed to be attested._

```solidity
function allowedAttestationTitles(string memory title) external view returns (bool);
```

### cannotReply

_Validates if an attestation can have a response._

```solidity
function cannotReply(bytes32 uid) external view returns (bool);
```

### allowedSchemas

_Checks which action a role can perform on a schema._

```solidity
function allowedSchemas(bytes32 uid) external view returns (Action);
```

### attest

Processes an attestation and verifies whether it's valid.

```solidity
function attest(Attestation calldata attestation) external payable returns (bool);
```

**Parameters**

| Name          | Type          | Description          |
| ------------- | ------------- | -------------------- |
| `attestation` | `Attestation` | The new attestation. |

**Returns**

| Name     | Type   | Description                       |
| -------- | ------ | --------------------------------- |
| `<none>` | `bool` | Whether the attestation is valid. |

### revoke

Processes an attestation revocation and verifies if it can be revoked.

```solidity
function revoke(Attestation calldata attestation) external payable returns (bool);
```

**Parameters**

| Name          | Type          | Description                             |
| ------------- | ------------- | --------------------------------------- |
| `attestation` | `Attestation` | The existing attestation to be revoked. |

**Returns**

| Name     | Type   | Description                             |
| -------- | ------ | --------------------------------------- |
| `<none>` | `bool` | Whether the attestation can be revoked. |

### getAllAttestationTitles

This function will retrieve all titles allowed in the resolver. It was designed to aid the frontend in displaying the current badges available. NOTE: Only the badges marked as valid will be returned.

```solidity
function getAllAttestationTitles() external view returns (string[] memory);
```

**Returns**

| Name     | Type       | Description                         |
| -------- | ---------- | ----------------------------------- |
| `<none>` | `string[]` | An array of all attestation titles. |

### setAttestationTitle

_Sets the attestation for a given title that will be attested. When creating attestions, the title must match to the desired configuration saved on the resolver._

```solidity
function setAttestationTitle(string memory title, bool isValid) external;
```

**Parameters**

| Name      | Type     | Description                                                               |
| --------- | -------- | ------------------------------------------------------------------------- |
| `title`   | `string` | The title of the attestation.                                             |
| `isValid` | `bool`   | Whether the title for the attestation is valid or not. Defaults to false. |

### setSchema

_Sets the action ID that schema can perform. The schema determines the data layout for the attestation, while the attestation determines the data that will fill the schema data._

```solidity
function setSchema(bytes32 uid, uint256 action) external;
```

**Parameters**

| Name     | Type      | Description                                         |
| -------- | --------- | --------------------------------------------------- |
| `uid`    | `bytes32` | The UID of the schema.                              |
| `action` | `uint256` | The action that the role can perform on the schema. |

## Enums

### Action

Actions that can be performed by the resolver.

```solidity
enum Action {
    NONE,
    ASSIGN_MANAGER,
    ASSIGN_VILLAGER,
    ATTEST,
    REPLY
}
```
