# Resolver
[Git Source](https://github.com/RafaDSan/trustful-zuzalu-contracts/blob/8145173dbd34bc00952ca1adb04b16dbe11ff624/src/resolver/Resolver.sol)

**Inherits:**
[IResolver](/src/interfaces/IResolver.sol/interface.IResolver.md), AccessControl

**Author:**
Blockful | 0xneves

ZuVillage Resolver contract for Ethereum Attestation Service.


## State Variables
### _eas

```solidity
IEAS internal immutable _eas;
```


### ROOT_ROLE

```solidity
bytes32 public constant ROOT_ROLE = keccak256("ROOT_ROLE");
```


### MANAGER_ROLE

```solidity
bytes32 public constant MANAGER_ROLE = keccak256("MANAGER_ROLE");
```


### VILLAGER_ROLE

```solidity
bytes32 public constant VILLAGER_ROLE = keccak256("VILLAGER_ROLE");
```


### _receivedManagerBadge

```solidity
mapping(address => bool) private _receivedManagerBadge;
```


### _allowedAttestationTitles

```solidity
mapping(bytes32 => bool) private _allowedAttestationTitles;
```


### _cannotReply

```solidity
mapping(bytes32 => bool) private _cannotReply;
```


### _allowedSchemas

```solidity
mapping(bytes32 => Action) private _allowedSchemas;
```


### _attestationTitles

```solidity
string[] private _attestationTitles;
```


## Functions
### constructor

*Creates a new resolver.*


```solidity
constructor(IEAS eas);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`eas`|`IEAS`|The address of the global EAS contract.|


### onlyEAS

*Ensures that only the EAS contract can make this call.*


```solidity
modifier onlyEAS();
```

### isPayable

Checks if the resolver can be sent ETH.


```solidity
function isPayable() public pure virtual returns (bool);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the resolver supports ETH transfers.|


### allowedAttestationTitles

*Checks if a title is allowed to be attested.*


```solidity
function allowedAttestationTitles(string memory title) public view returns (bool);
```

### cannotReply

*Validates if an attestation can have a response.*


```solidity
function cannotReply(bytes32 uid) public view returns (bool);
```

### allowedSchemas

*Checks which action a role can perform on a schema.*


```solidity
function allowedSchemas(bytes32 uid) public view returns (Action);
```

### isActionAllowed

*Validates if the `action` is allowed for the given `role` and `schema`.*


```solidity
function isActionAllowed(bytes32 uid, Action action) internal view returns (bool);
```

### attest

Processes an attestation and verifies whether it's valid.


```solidity
function attest(Attestation calldata attestation) external payable onlyEAS returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`attestation`|`Attestation`|The new attestation.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the attestation is valid.|


### revoke

Processes an attestation revocation and verifies if it can be revoked.


```solidity
function revoke(Attestation calldata attestation) external payable onlyEAS returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`attestation`|`Attestation`|The existing attestation to be revoked.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the attestation can be revoked.|


### assignManager

*Assign new managers to the contract.*


```solidity
function assignManager(Attestation calldata attestation) internal returns (bool);
```

### assignVillager

*Assign new villagers by checking in or revoke them by checking out.*


```solidity
function assignVillager(Attestation calldata attestation) internal returns (bool);
```

### attestEvent

*Attest an event badge.*


```solidity
function attestEvent(Attestation calldata attestation) internal view returns (bool);
```

### attestResponse

*Attest a response to an event badge emitted by [attestEvent](/src/resolver/Resolver.sol/contract.Resolver.md#attestevent).*


```solidity
function attestResponse(Attestation calldata attestation) internal returns (bool);
```

### getAllAttestationTitles

This function will retrieve all titles allowed in the resolver.
It was designed to aid the frontend in displaying the current badges available.
NOTE: Only the badges marked as valid will be returned.


```solidity
function getAllAttestationTitles() public view returns (string[] memory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`string[]`|An array of all attestation titles.|


### setAttestationTitle

*Sets the attestation for a given title that will be attested.
When creating attestions, the title must match to the desired configuration saved
on the resolver.*


```solidity
function setAttestationTitle(string memory title, bool isValid) public onlyRole(MANAGER_ROLE);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`title`|`string`|The title of the attestation.|
|`isValid`|`bool`|Whether the title for the attestation is valid or not. Defaults to false.|


### setSchema

*Sets the action ID that schema can perform.
The schema determines the data layout for the attestation, while the attestation
determines the data that will fill the schema data.*


```solidity
function setSchema(bytes32 uid, uint256 action) public onlyRole(ROOT_ROLE);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`uid`|`bytes32`|The UID of the schema.|
|`action`|`uint256`|The action that the role can perform on the schema.|


### receive

*ETH callback.*


```solidity
receive() external payable virtual;
```

