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

The `tokenURI` view renders an on-chain SVG preview of the bio string. A newline is automatically added every 40 characters, such that the bio is divided across up to 5 lines.

Note that newlines are not added at continutation bytes, zero-width joiners, or skin tone modifiers.