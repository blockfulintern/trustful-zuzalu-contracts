# Overview

> Trustful emerge

Trustful emerged to serve as a security layer for DAOs through reputation systems. The platform aims to transform traditional token-based voting power into a value-based approach, ushering in an era of [valocracy](https://mirror.xyz/research.blockful.eth/Ht7raeMRhVNg64X-uHJ3vowmox2Dx8_OPMWVWPnkVyI) in decentralized governance.

Currently, Trustful is in its early development stages as an MVP. The concept recently received validation at the Zuzalu Event in Georgia, though the project remains under active development.&#x20;

At this phase, Trustful has successfully implemented one of its foundational feature—statement badges—marking the beginning of its journey toward a groundbreaking reputational era.

### Sepolia

This environment houses the complete implementation of Statement Badges and Access Control mechanisms, providing stakeholders with a complete experience\[internal link to the video] with that Trustful has to offer at the moment.

### Optmism

The Optimism version was developed specifically for the Zuzalu ecosystem, serving as a use case during their in-person event. While this version remains exclusive to their ecosystem, it provided valuable validation and approval for Trustful's initial MVP

### Scroll

Trustful's deployment on the Scroll network serves as a testing playground for stakeholders. Although it's a simplified version compared to previous deployments, it allows users to freely experiment with the platform by issuing and receiving badges without restrictions.

<table data-view="cards"><thead><tr><th>Network</th><th></th></tr></thead><tbody><tr><td><img src="../.gitbook/assets/sepolia_ethereum_logo.png" alt="" data-size="line"> <strong><code>Sepolia</code></strong></td><td>                    ✅</td></tr><tr><td><img src="../.gitbook/assets/scroll_icon.png" alt="" data-size="line"><strong><code>Scroll</code></strong></td><td>                    ✅</td></tr><tr><td><img src="../.gitbook/assets/optimism-ethereum-op-logo.png" alt="" data-size="line"> <strong><code>Optmism</code></strong></td><td>                    ✅</td></tr></tbody></table>

***

## Core Features

### Statement Badges

* Issue a badge to someone's address stating something about another address using the Ethereum Attestation Service, but only if both addresses are villagers and the badge title has been previously approved by a manager
* These badges must use pre-determined titles that are explicitly allowed by managers - custom titles are not permitted unless first registered
* It is possible to issue with two components: a title and a comment
* These badges are non-revocable (they are permanent)
* Other addresses that are villagers can respond to these badges with a single response and these responses are revocable
* Other addresses that are villagers can respond to these badges with a single response and these responses are revocable

### Access Control

ROOT

* Primary administrator role with complete system control
* Can assign and revoke Manager badges
* Manages role assignments and removals
* Configures EAS schema actions that define core dApp behavior

MANAGER

* Event administration role focused on participant management
* Controls participant check-in and check-out processes
* Can assign and revoke Manager badges
* Defines and manages the allowed badge titles within the system

VILLAGER

* Standard participant role for event attendees
* Can issue badges to other participants
* Can respond to received badges
* Can check out of the dApp
