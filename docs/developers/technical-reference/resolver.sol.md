# Resolver.sol

[Git Source](https://github.com/RafaDSan/trustful-zuzalu-contracts/blob/8145173dbd34bc00952ca1adb04b16dbe11ff624/src/resolver/Resolver.sol)

**Inherits:** [IResolver](../../../src/interfaces/IResolver.sol/interface.IResolver.md), AccessControl

Resolver contract for Ethereum Attestation Service.

## State Variables

### \_eas

```solidity
IEAS internal immutable _eas;
```

### ROOT\_ROLE

```solidity
bytes32 public constant ROOT_ROLE = keccak256("ROOT_ROLE");
```

### MANAGER\_ROLE

```solidity
bytes32 public constant MANAGER_ROLE = keccak256("MANAGER_ROLE");
```

### VILLAGER\_ROLE

```solidity
bytes32 public constant VILLAGER_ROLE = keccak256("VILLAGER_ROLE");
```

### \_receivedManagerBadge

```solidity
mapping(address => bool) private _receivedManagerBadge;
```

### \_allowedAttestationTitles

```solidity
mapping(bytes32 => bool) private _allowedAttestationTitles;
```

### \_cannotReply

```solidity
mapping(bytes32 => bool) private _cannotReply;
```

### \_allowedSchemas

```solidity
mapping(bytes32 => Action) private _allowedSchemas;
```

### \_attestationTitles

```solidity
string[] private _attestationTitles;
```

## Functions

### constructor

_Creates a new resolver._

```solidity
constructor(IEAS eas);
```

**Parameters**

| Name  | Type   | Description                             |
| ----- | ------ | --------------------------------------- |
| `eas` | `IEAS` | The address of the global EAS contract. |

### onlyEAS

_Ensures that only the EAS contract can make this call._

```solidity
modifier onlyEAS();
```

### isPayable

Checks if the resolver can be sent ETH.

```solidity
function isPayable() public pure virtual returns (bool);
```

**Returns**

| Name     | Type   | Description                                  |
| -------- | ------ | -------------------------------------------- |
| `<none>` | `bool` | Whether the resolver supports ETH transfers. |

### allowedAttestationTitles

_Checks if a title is allowed to be attested._

```solidity
function allowedAttestationTitles(string memory title) public view returns (bool);
```

### cannotReply

_Validates if an attestation can have a response._

```solidity
function cannotReply(bytes32 uid) public view returns (bool);
```

### allowedSchemas

_Checks which action a role can perform on a schema._

```solidity
function allowedSchemas(bytes32 uid) public view returns (Action);
```

### isActionAllowed

_Validates if the `action` is allowed for the given `role` and `schema`._

```solidity
function isActionAllowed(bytes32 uid, Action action) internal view returns (bool);
```

### attest

Processes an attestation and verifies whether it's valid.

```solidity
function attest(Attestation calldata attestation) external payable onlyEAS returns (bool);
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
function revoke(Attestation calldata attestation) external payable onlyEAS returns (bool);
```

**Parameters**

| Name          | Type          | Description                             |
| ------------- | ------------- | --------------------------------------- |
| `attestation` | `Attestation` | The existing attestation to be revoked. |

**Returns**

| Name     | Type   | Description                             |
| -------- | ------ | --------------------------------------- |
| `<none>` | `bool` | Whether the attestation can be revoked. |

### assignManager

_Assign new managers to the contract._

```solidity
function assignManager(Attestation calldata attestation) internal returns (bool);
```

### assignVillager

_Assign new villagers by checking in or revoke them by checking out._

```solidity
function assignVillager(Attestation calldata attestation) internal returns (bool);
```

### attestEvent

_Attest an event badge._

```solidity
function attestEvent(Attestation calldata attestation) internal view returns (bool);
```

### attestResponse

_Attest a response to an event badge emitted by_ [_attestEvent_](../../../src/resolver/Resolver.sol/contract.Resolver.md#attestevent)_._

```solidity
function attestResponse(Attestation calldata attestation) internal returns (bool);
```

### getAllAttestationTitles

This function will retrieve all titles allowed in the resolver. It was designed to aid the frontend in displaying the current badges available. NOTE: Only the badges marked as valid will be returned.

```solidity
function getAllAttestationTitles() public view returns (string[] memory);
```

**Returns**

| Name     | Type       | Description                         |
| -------- | ---------- | ----------------------------------- |
| `<none>` | `string[]` | An array of all attestation titles. |

### setAttestationTitle

_Sets the attestation for a given title that will be attested. When creating attestions, the title must match to the desired configuration saved on the resolver._

```solidity
function setAttestationTitle(string memory title, bool isValid) public onlyRole(MANAGER_ROLE);
```

**Parameters**

| Name      | Type     | Description                                                               |
| --------- | -------- | ------------------------------------------------------------------------- |
| `title`   | `string` | The title of the attestation.                                             |
| `isValid` | `bool`   | Whether the title for the attestation is valid or not. Defaults to false. |

### setSchema

_Sets the action ID that schema can perform. The schema determines the data layout for the attestation, while the attestation determines the data that will fill the schema data._

```solidity
function setSchema(bytes32 uid, uint256 action) public onlyRole(ROOT_ROLE);
```

**Parameters**

| Name     | Type      | Description                                         |
| -------- | --------- | --------------------------------------------------- |
| `uid`    | `bytes32` | The UID of the schema.                              |
| `action` | `uint256` | The action that the role can perform on the schema. |

### receive

_ETH callback._

```solidity
receive() external payable virtual;
```
