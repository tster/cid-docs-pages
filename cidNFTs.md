# Canto Identity NFTs

Canto Identity NFTs (cidNFTs) represent individual on-chain identities. Through nested mappings, they point to subprotocolNFTs representing individual identity traits.

On `CidNFT.sol`, the internal mapping `cidData` maps cidNFT tokenIds to Subprotocols, which in turn map to `SubprotocolData` structs:

```solidity
mapping(uint256 => mapping(string => SubprotocolData)) internal cidData;
```

The `SubprotocolData` struct is composed of three types corresponding to each of the three [Association Types](subprotocol-creation.md#association-types) a Subprotocol may use:

```solidity
    struct SubprotocolData {
        /// @notice Mapping for ordered type
        mapping(uint256 => uint256) ordered;
        /// @notice Value for primary type
        uint256 primary;
        /// @notice List for active type
        IndexedArray active;
    }
```

* The `ordered` type is a mapping which maps indexes (0,1,2...) to subprotocolNFT tokenIds
* The `primary` type is a tokenId for a single subprotocolNFT
* the `active` type is a struct consisting of an array of subprotocolNFT tokenIds and a mapping which maps the tokenIds to a non-zero index (1,2...)

## Reading cidNFTs

To retrieve the subprotocolNFTs a cidNFT to points to for a specified Subprotocol, `CidNFT.sol` has three external views – one for each association type:

* `getOrderedData` takes a cidNFT tokenId, Subprotocol name, and index and returns a subprotocolNFT tokenId
* `getPrimaryData` takes a cidNFT tokenId and Subprotocol name and returns a subprotocolNFT tokenID
* `getActiveData` takes a cidNFT tokenId and Subprotocol name and returns an array of subprotocolNFT tokenIds

## Adding and Removing subprotocolNFTs

Users can add pointers to subprotocolNFTs to their cidNFTs by calling the `add` function on `CidNFT.sol`. They must provide:

* `_cidNFTID`, the tokenId of the cidNFT
* `_subProtocolName`, the name of the Subprotocol
* `_key`, the key to be used for the pointer (only used for the `ordered` association type)
* `_nftIDToAdd`, the tokenId of the subprotocolNFTs
* `_type`, the type of association being made

The smart contract performs numerous checks before adding the pointer to `cidData` and emitting an event.

Users can remove pointers to subprotocolNFTs from their cidNFTs by calling the `remove` function on `CidNFT.sol` with the same inputs.

## Registering and Retrieving cidNFTs

Users register a cidNFT as their canonical on-chain identity with the `register` method on `AddressRegistry.sol`, providing only the cidNFT's tokenId. To remove a registration, users can call the `remove` method.

Note that a wallet can only have one CidNFT registered to its address at any given time.

The `getCid` method on `AddressRegistry.sol` retrieves the tokenId of the cidNFT registered to a specified address. If no cidNFT is registered to an address, this method returns `0`.