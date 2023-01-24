# Subprotocol Development & Registration

Canto Identity Subprotocols are loosely defined smart contracts which use NFTs called subprotocolNFTs to represent identity traits. Users include these identity traits in their on-chain identities by adding pointers to them to their cidNFTs.

The interface for Subprotocols is based on the [Solmate ERC721 standard](https://github.com/transmissions11/solmate/blob/main/src/tokens/ERC721.sol) and is outlined in `CidSubprotocolNFT.sol`:

```solidity
import "solmate/tokens/ERC721.sol";

abstract contract CidSubprotocolNFT is ERC721 {
    bytes4 internal constant CID_SUBPROTOCOL_INTERFACE_ID = type(CidSubprotocolNFT).interfaceId;

    /// @notice Returns if a subprotocol NFT is still active. Subprotocol NFTs may be a pointer to a different entity (e.g., another NFT)
    /// and this entity may no longer exist or may no longer be owned by the owner of the subprotocol NFT, in which case false should be returned.
    /// @dev Has to revert if the given NFT ID does not exist
    /// @param _nftID Subprotocol NFT ID to query
    /// @return active True if the Subprotocol NFT should be considered active
    function isActive(uint256 _nftID) public virtual returns (bool active);

    function supportsInterface(bytes4 interfaceId) public pure override returns (bool) {
        return interfaceId == CID_SUBPROTOCOL_INTERFACE_ID || super.supportsInterface(interfaceId);
    }
}
```

Subprotocol creators can introduce arbitrary minting and ownership logic to their Subprotocols so long as they conform to `CidSubprotocolNFT.sol` and its parent Solmate ERC721 contract.

## Subprotocol Registration

Subprotocols must be registered with `SubprotocolRegistry.sol` for a one-time fee in order to be used within Canto Identity Protocol. The `register` function takes the following inputs:

* `_ordered`, a boolean specifiying whether the Subprotocol uses the `ordered` Association Type
* `_primary`, a boolean specifiying whether the Subprotocol uses the `ordered` Association Type
* `_active`, a boolean specifiying whether the Subprotocol uses the `ordered` Association Type
* `_nftAddress`, the smart contract address of the Subprotocol
* `_name`, a unique name for the Subprotocol
* `_fee`, the fee in $NOTE to mint a subprotocolNFT

### Association Types

For each Subprotcol, subprotocolNFTs associate with cidNFTs according to three mutually inclusive Association Types:
- `primary`: no more than one subprotocolNFT can be added to a cidNFT
- `active`: the subprotocolNFTs may be active or inactive at any time
- `ordered`: the subprotocolNFTs added to a cidNFT are strictly ordered

The Assocation Types used by a Subprotocol are specified by the Subprotocol creator at registration based on how the Subprotocol is intended to be used.

### Registration Fee

A one-time 100 $NOTE registration fee is charged when registering a Subprotocol. Before calling the `register` method, the Subprotocol creator should ensure they have approved $NOTE to `SubprotocolRegistry.sol` and have the required number of tokens in their wallet.