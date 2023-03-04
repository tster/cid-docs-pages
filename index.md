---
nav_order: 0
---

# Overview

Canto Identity Protocol (CID) is a permisionless protocol that reinvents the concept of on-chain identity. With CID, the power to control one's on-chain identity is returned to users.

At launch, the core CID protocol consists of three smart contracts:
- [`AddressRegistry.sol`](https://github.com/mkt-market/canto-identity-protocol/blob/master/src/AddressRegistry.sol)
- [`CidNFT.sol`](https://github.com/mkt-market/canto-identity-protocol/blob/master/src/CidNFT.sol)
- [`SubprotocolRegistry.sol`](https://github.com/mkt-market/canto-identity-protocol/blob/master/src/SubprotocolRegistry.sol)

Within Canto Identity Protocol, ERC721 NFTs called [cidNFTs](cidNFTs.md) represent individual on-chain identities. Users can mint cidNFTs for free by calling the `mint` method on `CidNFT.sol`.

Users must [register](cidNFTs.md#registering-cidnfts) a cidNFT as their canonical on-chain identity with `AddressRegistry.sol`.

## Subprotocols

The core Canto Identity Protocol has no notion of identity traits, such as display name. Instead, it aggregates identity from granular, trait-specific protocols called Subprotocols.

[Subprotocol creation](subprotocols.md) is permissionless. However, subprotocols must be [registered](subprotocols.md#subprotocol-registration) with `SubprotocolRegistry.sol` for a one-time fee in order to be used within Canto Identity Protocol.

### subprotocolNFTs

subprotocolNFTs represent individual identity traits. Users choose which traits to include in their on-chain identity by adding references to those subprotocolNFTs to their cidNFT using the `add` method on `CidNFT.sol`.

Fees and conditions associated with minting subprotocolNFTs are determined by the Subprotocol's creator. Since Subprotocols are loosely defined smart contracts, Subprotocol creators can introduce arbitrary logic to NFT minting and ownership.