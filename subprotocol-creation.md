---
nav_order: 2
---

# Subprotocol Development & Registration

Canto Identity Subprotocols are smart contracts which use NFTs called subprotocolNFTs to represent identity traits. Users include these identity traits in their on-chain identities by adding pointers to them to their cidNFTs.

Subprotocols should implement the ERC721 standard, but there is no strict interface they must conform to. As a result, subprotocol creators can introduce arbitrary minting and ownership logic.

## Subprotocol Registration

Subprotocols must be registered with `SubprotocolRegistry.sol` for a one-time fee in order to be used within Canto Identity Protocol. The `register` function takes the following inputs:

* `_ordered`, a boolean specifiying whether the Subprotocol uses the `ordered` Association Type
* `_primary`, a boolean specifiying whether the Subprotocol uses the `primary` Association Type
* `_active`, a boolean specifiying whether the Subprotocol uses the `active` Association Type
* `_nftAddress`, the smart contract address of the Subprotocol
* `_name`, a unique name for the Subprotocol
* `_fee`, the fee in $NOTE to mint a subprotocolNFT

### Association Types

For each Subprotcol, subprotocolNFTs associate with cidNFTs according to three mutually inclusive Association Types:
- `primary`: no more than one subprotocolNFT can be added to a cidNFT
- `active`: the subprotocolNFTs added to a cidNFT have no order
- `ordered`: the subprotocolNFTs added to a cidNFT are strictly ordered

The Assocation Types used by a Subprotocol are specified by the Subprotocol creator at registration based on how the Subprotocol is intended to be used.

### Registration Fee

A one-time 100 $NOTE registration fee is charged when registering a Subprotocol. Before calling the `register` method, the Subprotocol creator should ensure they have approved $NOTE to `SubprotocolRegistry.sol` and have the required number of tokens in their wallet.