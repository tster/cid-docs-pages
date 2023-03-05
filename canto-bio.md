---
nav_order: 1
parent: Subprotocols
---

# Canto Bio Protocol

Canto Bio Protocol is a barebones Subprotocol that can be used to save a *bio* string in one's on-chain identity. It consists of a single smart contract, `Bio.sol`.

## Minting

To mint a Bio subprotocolNFT, a user calls `mint` on the smart contract, passing in a string. The string can contain any characters (letters, punctuation, emojis) but its length must be between 1 and 199 bytes.

Upper- and lowercase Latin characters as well as basic punctuation and control codes (Basic Latin) can be encoded in one byte, so the practical character limit for simple bio strings is 199 characters.

## Bio Preview

The `tokenURI` method takes a Bio subprotocolNFT tokenId and renders an on-chain SVG preview of that bio string.