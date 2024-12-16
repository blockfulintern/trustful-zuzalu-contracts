# Overview

## Run your local Trustful

Follow through this guide to learn how to run the Trustful locally

***

### Access Control

The system implements three distinct roles through OpenZeppelin's AccessControl:

* `ROOT_ROLE`: The highest administrative level, defined as `keccak256("ROOT_ROLE")`
* `MANAGER_ROLE`: Event operators, defined as `keccak256("MANAGER_ROLE")`
* `VILLAGER_ROLE`: Participants, defined as `keccak256("VILLAGER_ROLE")`

The `ROOT_ROLE` serves as the admin for all roles, as established in the constructor through `_setRoleAdmin()` calls.

### Statement Badges

Statement badges are the fundamental unit of reputation in Trustful, implemented as EAS attestations.

* Badge issuance is restricted to addresses with `VILLAGER_ROLE`, enforced by `_checkRole()` in the `attestEvent` function
* Most badges are permanent and non-revocable, verified by the `if (attestation.revocable) revert InvalidRevocability()` check.&#x20;
  * Obs: Only the manager and reply badge are revocable.
* Response functionality is controlled through the `_cannotReply` mapping, allowing only one active response per attestation
* Responses must be revocable as enforced by `if (!attestation.revocable) revert InvalidRevocability()`

### Ethereum Attestation Service (EAS) integration

Trustful leverages EAS as its core infrastructure.

<details>

<summary>Attestation Types</summary>

* Manager assignments
* Villager status (check-in/out)
* Badge issuance
* Badge responses

</details>

* Badge issuance is restricted to addresses with `VILLAGER_ROLE`, enforced by `_checkRole()` in the `attestEvent` function
* Badges are permanent and non-revocable, verified by the `if (attestation.revocable) revert InvalidRevocability()` check
* Response functionality is controlled through the `_cannotReply` mapping, allowing only one active response per attestation
* Responses must be revocable as enforced by `if (!attestation.revocable) revert InvalidRevocability()`

### Schema Management

Schemas define the structure and rules for different attestation types:

<details>

<summary>Action Types</summary>

* NONE
* ASSIGN\_MANAGER
* ASSIGN\_VILLAGER
* ATTEST
* REPLY

</details>

* The `_allowedSchemas` mapping that connects schema UIDs to specific actions
* The `setSchema` function, restricted to `ROOT_ROLE`, for registering valid schemas
* Action validation through `isActionAllowed` internal function
* Five distinct actions: NONE`, ASSIGN_MANAGER`, `ASSIGN_VILLAGER`, `ATTEST`, and `REPLY`

### Attestation Titles

Manages the registry of allowed badge titles:

* The `_allowedAttestationTitles` mapping tracking valid titles
* `setAttestationTitle` function restricted to `MANAGER_ROLE`
* `_attestationTitles` array storing all registered titles
* Title validation in `attestEvent` through `_allowedAttestationTitles[keccak256(abi.encode(title))]`
* `getAllAttestationTitles()` function for retrieving all valid titles





