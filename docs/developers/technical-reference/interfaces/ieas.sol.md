# IEAS.sol

[Git Source](https://github.com/RafaDSan/trustful-zuzalu-contracts/blob/8145173dbd34bc00952ca1adb04b16dbe11ff624/src/interfaces/IEAS.sol)

**Inherits:** [ISemver](../../../../src/interfaces/ISemver.sol/interface.ISemver.md)

EAS - Ethereum Attestation Service interface.

## Functions

### getSchemaRegistry

Returns the address of the global schema registry.

```solidity
function getSchemaRegistry() external view returns (ISchemaRegistry);
```

**Returns**

| Name     | Type              | Description                                |
| -------- | ----------------- | ------------------------------------------ |
| `<none>` | `ISchemaRegistry` | The address of the global schema registry. |

### attest

Attests to a specific schema.

```solidity
function attest(AttestationRequest calldata request) external payable returns (bytes32);
```

**Parameters**

| Name      | Type                 | Description                               |
| --------- | -------------------- | ----------------------------------------- |
| `request` | `AttestationRequest` | The arguments of the attestation request. |

**Returns**

| Name     | Type      | Description                                                                                                                                                                                                                                                                                                                                    |
| -------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<none>` | `bytes32` | The UID of the new attestation. Example: attest({ schema: "0facc36681cbe2456019c1b0d1e7bedd6d1d40f6f324bf3dd3a4cef2999200a0", data: { recipient: "0xdEADBeAFdeAdbEafdeadbeafDeAdbEAFdeadbeaf", expirationTime: 0, revocable: true, refUID: "0x0000000000000000000000000000000000000000000000000000000000000000", data: "0xF00D", value: 0 } }) |

### attestByDelegation

Attests to a specific schema via the provided ECDSA signature.

```solidity
function attestByDelegation(DelegatedAttestationRequest calldata delegatedRequest) external payable returns (bytes32);
```

**Parameters**

| Name               | Type                          | Description                                         |
| ------------------ | ----------------------------- | --------------------------------------------------- |
| `delegatedRequest` | `DelegatedAttestationRequest` | The arguments of the delegated attestation request. |

**Returns**

| Name     | Type      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<none>` | `bytes32` | The UID of the new attestation. Example: attestByDelegation({ schema: '0x8e72f5bc0a8d4be6aa98360baa889040c50a0e51f32dbf0baa5199bd93472ebc', data: { recipient: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266', expirationTime: 1673891048, revocable: true, refUID: '0x0000000000000000000000000000000000000000000000000000000000000000', data: '0x1234', value: 0 }, signature: { v: 28, r: '0x148c...b25b', s: '0x5a72...be22' }, attester: '0xc5E8740aD971409492b1A63Db8d83025e0Fc427e', deadline: 1673891048 }) |

### multiAttest

Attests to multiple schemas.

```solidity
function multiAttest(MultiAttestationRequest[] calldata multiRequests) external payable returns (bytes32[] memory);
```

**Parameters**

| Name            | Type                        | Description                                                                                                                                            |
| --------------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `multiRequests` | `MultiAttestationRequest[]` | The arguments of the multi attestation requests. The requests should be grouped by distinct schema ids to benefit from the best batching optimization. |

**Returns**

| Name     | Type        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| -------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `<none>` | `bytes32[]` | The UIDs of the new attestations. Example: multiAttest(\[{ schema: '0x33e9094830a5cba5554d1954310e4fbed2ef5f859ec1404619adea4207f391fd', data: \[{ recipient: '0xdEADBeAFdeAdbEafdeadbeafDeAdbEAFdeadbeaf', expirationTime: 1673891048, revocable: true, refUID: '0x0000000000000000000000000000000000000000000000000000000000000000', data: '0x1234', value: 1000 }, { recipient: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266', expirationTime: 0, revocable: false, refUID: '0x480df4a039efc31b11bfdf491b383ca138b6bde160988222a2a3509c02cee174', data: '0x00', value: 0 }], }, { schema: '0x5ac273ce41e3c8bfa383efe7c03e54c5f0bff29c9f11ef6ffa930fc84ca32425', data: \[{ recipient: '0xdEADBeAFdeAdbEafdeadbeafDeAdbEAFdeadbeaf', expirationTime: 0, revocable: true, refUID: '0x75bf2ed8dca25a8190c50c52db136664de25b2449535839008ccfdab469b214f', data: '0x12345678', value: 0 }, }]) |

### multiAttestByDelegation

Attests to multiple schemas using via provided ECDSA signatures.

```solidity
function multiAttestByDelegation(MultiDelegatedAttestationRequest[] calldata multiDelegatedRequests)
    external
    payable
    returns (bytes32[] memory);
```

**Parameters**

| Name                     | Type                                 | Description                                                                                                                                                      |
| ------------------------ | ------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `multiDelegatedRequests` | `MultiDelegatedAttestationRequest[]` | The arguments of the delegated multi attestation requests. The requests should be grouped by distinct schema ids to benefit from the best batching optimization. |

**Returns**

| Name     | Type        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<none>` | `bytes32[]` | The UIDs of the new attestations. Example: multiAttestByDelegation(\[{ schema: '0x8e72f5bc0a8d4be6aa98360baa889040c50a0e51f32dbf0baa5199bd93472ebc', data: \[{ recipient: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266', expirationTime: 1673891048, revocable: true, refUID: '0x0000000000000000000000000000000000000000000000000000000000000000', data: '0x1234', value: 0 }, { recipient: '0xdEADBeAFdeAdbEafdeadbeafDeAdbEAFdeadbeaf', expirationTime: 0, revocable: false, refUID: '0x0000000000000000000000000000000000000000000000000000000000000000', data: '0x00', value: 0 }], signatures: \[{ v: 28, r: '0x148c...b25b', s: '0x5a72...be22' }, { v: 28, r: '0x487s...67bb', s: '0x12ad...2366' }], attester: '0x1D86495b2A7B524D747d2839b3C645Bed32e8CF4', deadline: 1673891048 }]) |

### revoke

Revokes an existing attestation to a specific schema.

```solidity
function revoke(RevocationRequest calldata request) external payable;
```

**Parameters**

| Name      | Type                | Description                                                                                                                                                                                                                               |
| --------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `request` | `RevocationRequest` | The arguments of the revocation request. Example: revoke({ schema: '0x8e72f5bc0a8d4be6aa98360baa889040c50a0e51f32dbf0baa5199bd93472ebc', data: { uid: '0x101032e487642ee04ee17049f99a70590c735b8614079fc9275f9dd57c00966d', value: 0 } }) |

### revokeByDelegation

Revokes an existing attestation to a specific schema via the provided ECDSA signature.

```solidity
function revokeByDelegation(DelegatedRevocationRequest calldata delegatedRequest) external payable;
```

**Parameters**

| Name               | Type                         | Description                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------ | ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `delegatedRequest` | `DelegatedRevocationRequest` | The arguments of the delegated revocation request. Example: revokeByDelegation({ schema: '0x8e72f5bc0a8d4be6aa98360baa889040c50a0e51f32dbf0baa5199bd93472ebc', data: { uid: '0xcbbc12102578c642a0f7b34fe7111e41afa25683b6cd7b5a14caf90fa14d24ba', value: 0 }, signature: { v: 27, r: '0xb593...7142', s: '0x0f5b...2cce' }, revoker: '0x244934dd3e31bE2c81f84ECf0b3E6329F5381992', deadline: 1673891048 }) |

### multiRevoke

Revokes existing attestations to multiple schemas.

```solidity
function multiRevoke(MultiRevocationRequest[] calldata multiRequests) external payable;
```

**Parameters**

| Name            | Type                       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --------------- | -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `multiRequests` | `MultiRevocationRequest[]` | The arguments of the multi revocation requests. The requests should be grouped by distinct schema ids to benefit from the best batching optimization. Example: multiRevoke(\[{ schema: '0x8e72f5bc0a8d4be6aa98360baa889040c50a0e51f32dbf0baa5199bd93472ebc', data: \[{ uid: '0x211296a1ca0d7f9f2cfebf0daaa575bea9b20e968d81aef4e743d699c6ac4b25', value: 1000 }, { uid: '0xe160ac1bd3606a287b4d53d5d1d6da5895f65b4b4bab6d93aaf5046e48167ade', value: 0 }], }, { schema: '0x5ac273ce41e3c8bfa383efe7c03e54c5f0bff29c9f11ef6ffa930fc84ca32425', data: \[{ uid: '0x053d42abce1fd7c8fcddfae21845ad34dae287b2c326220b03ba241bc5a8f019', value: 0 }, }]) |

### multiRevokeByDelegation

Revokes existing attestations to multiple schemas via provided ECDSA signatures.

```solidity
function multiRevokeByDelegation(MultiDelegatedRevocationRequest[] calldata multiDelegatedRequests) external payable;
```

**Parameters**

| Name                     | Type                                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------ | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `multiDelegatedRequests` | `MultiDelegatedRevocationRequest[]` | The arguments of the delegated multi revocation attestation requests. The requests should be grouped by distinct schema ids to benefit from the best batching optimization. Example: multiRevokeByDelegation(\[{ schema: '0x8e72f5bc0a8d4be6aa98360baa889040c50a0e51f32dbf0baa5199bd93472ebc', data: \[{ uid: '0x211296a1ca0d7f9f2cfebf0daaa575bea9b20e968d81aef4e743d699c6ac4b25', value: 1000 }, { uid: '0xe160ac1bd3606a287b4d53d5d1d6da5895f65b4b4bab6d93aaf5046e48167ade', value: 0 }], signatures: \[{ v: 28, r: '0x148c...b25b', s: '0x5a72...be22' }, { v: 28, r: '0x487s...67bb', s: '0x12ad...2366' }], revoker: '0x244934dd3e31bE2c81f84ECf0b3E6329F5381992', deadline: 1673891048 }]) |

### timestamp

Timestamps the specified bytes32 data.

```solidity
function timestamp(bytes32 data) external returns (uint64);
```

**Parameters**

| Name   | Type      | Description            |
| ------ | --------- | ---------------------- |
| `data` | `bytes32` | The data to timestamp. |

**Returns**

| Name     | Type     | Description                                  |
| -------- | -------- | -------------------------------------------- |
| `<none>` | `uint64` | The timestamp the data was timestamped with. |

### multiTimestamp

Timestamps the specified multiple bytes32 data.

```solidity
function multiTimestamp(bytes32[] calldata data) external returns (uint64);
```

**Parameters**

| Name   | Type        | Description            |
| ------ | ----------- | ---------------------- |
| `data` | `bytes32[]` | The data to timestamp. |

**Returns**

| Name     | Type     | Description                                  |
| -------- | -------- | -------------------------------------------- |
| `<none>` | `uint64` | The timestamp the data was timestamped with. |

### revokeOffchain

Revokes the specified bytes32 data.

```solidity
function revokeOffchain(bytes32 data) external returns (uint64);
```

**Parameters**

| Name   | Type      | Description            |
| ------ | --------- | ---------------------- |
| `data` | `bytes32` | The data to timestamp. |

**Returns**

| Name     | Type     | Description                              |
| -------- | -------- | ---------------------------------------- |
| `<none>` | `uint64` | The timestamp the data was revoked with. |

### multiRevokeOffchain

Revokes the specified multiple bytes32 data.

```solidity
function multiRevokeOffchain(bytes32[] calldata data) external returns (uint64);
```

**Parameters**

| Name   | Type        | Description            |
| ------ | ----------- | ---------------------- |
| `data` | `bytes32[]` | The data to timestamp. |

**Returns**

| Name     | Type     | Description                              |
| -------- | -------- | ---------------------------------------- |
| `<none>` | `uint64` | The timestamp the data was revoked with. |

### getAttestation

Returns an existing attestation by UID.

```solidity
function getAttestation(bytes32 uid) external view returns (Attestation memory);
```

**Parameters**

| Name  | Type      | Description                             |
| ----- | --------- | --------------------------------------- |
| `uid` | `bytes32` | The UID of the attestation to retrieve. |

**Returns**

| Name     | Type          | Description                   |
| -------- | ------------- | ----------------------------- |
| `<none>` | `Attestation` | The attestation data members. |

### isAttestationValid

Checks whether an attestation exists.

```solidity
function isAttestationValid(bytes32 uid) external view returns (bool);
```

**Parameters**

| Name  | Type      | Description                             |
| ----- | --------- | --------------------------------------- |
| `uid` | `bytes32` | The UID of the attestation to retrieve. |

**Returns**

| Name     | Type   | Description                    |
| -------- | ------ | ------------------------------ |
| `<none>` | `bool` | Whether an attestation exists. |

### getTimestamp

Returns the timestamp that the specified data was timestamped with.

```solidity
function getTimestamp(bytes32 data) external view returns (uint64);
```

**Parameters**

| Name   | Type      | Description        |
| ------ | --------- | ------------------ |
| `data` | `bytes32` | The data to query. |

**Returns**

| Name     | Type     | Description                                  |
| -------- | -------- | -------------------------------------------- |
| `<none>` | `uint64` | The timestamp the data was timestamped with. |

### getRevokeOffchain

Returns the timestamp that the specified data was timestamped with.

```solidity
function getRevokeOffchain(address revoker, bytes32 data) external view returns (uint64);
```

**Parameters**

| Name      | Type      | Description        |
| --------- | --------- | ------------------ |
| `revoker` | `address` |                    |
| `data`    | `bytes32` | The data to query. |

**Returns**

| Name     | Type     | Description                                  |
| -------- | -------- | -------------------------------------------- |
| `<none>` | `uint64` | The timestamp the data was timestamped with. |

## Events

### Attested

Emitted when an attestation has been made.

```solidity
event Attested(address indexed recipient, address indexed attester, bytes32 uid, bytes32 indexed schemaUID);
```

**Parameters**

| Name        | Type      | Description                       |
| ----------- | --------- | --------------------------------- |
| `recipient` | `address` | The recipient of the attestation. |
| `attester`  | `address` | The attesting account.            |
| `uid`       | `bytes32` | The UID of the new attestation.   |
| `schemaUID` | `bytes32` | The UID of the schema.            |

### Revoked

Emitted when an attestation has been revoked.

```solidity
event Revoked(address indexed recipient, address indexed attester, bytes32 uid, bytes32 indexed schemaUID);
```

**Parameters**

| Name        | Type      | Description                       |
| ----------- | --------- | --------------------------------- |
| `recipient` | `address` | The recipient of the attestation. |
| `attester`  | `address` | The attesting account.            |
| `uid`       | `bytes32` | The UID the revoked attestation.  |
| `schemaUID` | `bytes32` | The UID of the schema.            |

### Timestamped

Emitted when a data has been timestamped.

```solidity
event Timestamped(bytes32 indexed data, uint64 indexed timestamp);
```

**Parameters**

| Name        | Type      | Description    |
| ----------- | --------- | -------------- |
| `data`      | `bytes32` | The data.      |
| `timestamp` | `uint64`  | The timestamp. |

### RevokedOffchain

Emitted when a data has been revoked.

```solidity
event RevokedOffchain(address indexed revoker, bytes32 indexed data, uint64 indexed timestamp);
```

**Parameters**

| Name        | Type      | Description                 |
| ----------- | --------- | --------------------------- |
| `revoker`   | `address` | The address of the revoker. |
| `data`      | `bytes32` | The data.                   |
| `timestamp` | `uint64`  | The timestamp.              |
