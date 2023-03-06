---
nav_order: 0
parent: Subprotocols
---

# Canto PFP Protocol

Canto PFP Protocol is a barebones Subprotocol that can be used to reference any ERC721 NFT in one's on-chain identity. It consists of a single smart contract, `ProfilePicture.sol`.

## Minting

To mint a PFP subprotocolNFT, a user calls `mint` on the smart contract, passing in the address of an NFT collection and the tokenId of an NFT they hold from that collection.

The `mint` method reverts if the user is not holding the referenced NFT in their wallet.

## Ownership Checks

The `getPFP` method checks whether the NFT referenced by a PFP subprotocolNFT is still owned by the expected wallet. It uses `CidNFT.sol` to lookup which cidNFT the PFP subprotocolNFT has been added to, after which it performs an ownership check against the address that cidNFT resolves to on `AddressRegistry.sol`.

If the NFT is still owned by the expected wallet, this method returns the address of the NFT collection and the tokenId of the NFT. Otherwise, it returns `address(0)` and `0` respectively.

## PFP Preview and Metadata

The `tokenURI` view calls `getPFP` internally. If the referenced NFT is owned by the expected wallet, it returns the tokenURI of the referenced NFT. Otherwise, it reverts.

In practice, this means that the PFP subprotocolNFT shares the same metadata (including image) as the referenced NFT if that NFT is owned by the expected wallet.