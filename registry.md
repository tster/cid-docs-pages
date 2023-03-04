---
nav_order: 2
---

# Address Registry

`AddressRegistry.sol` allows users to register a cidNFT as their canonical on-chain identity. It also offers address lookup and reverse lookup functionality, allowing applications to find an address' registered cidNFT and vice versa.

## Registering cidNFTs

To register a cidNFT to an address, users must call the `register` method on `AddressRegistry.sol`, passing in the cidNFT's tokenId. To remove a registration, users can call the `remove` method.

Note that a wallet can only have one cidNFT registered to its address at any given time. Calling the `register` method from a wallet address that has already registered a cidNFT will overwrite its existing registration.

Transferring a cidNFT to another wallet will remove its existing registration.

## Address Lookup

The `getCid` method takes an address and returns the tokenId of the cidNFT registered to that address. If no cidNFT is registered to the address, this method returns `0`.

### Reverse Lookup

The `getAddress` method takes a tokenId (of a cidNFT) and returns the address to which it is registered. If the queried cidNFT is not registered to an address, this method returns `address(0)`.